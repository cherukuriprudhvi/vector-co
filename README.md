

/* =========================================================
   CAN1 - 12V EPAS TEST
   Sends BOTH:
     0x213 EnergyMgmtBodyCtrl_4
     0x203 EnergyMgmtBodyInfo_4

   Sequence:
   OFF      1 sec
   STANDBY  2 sec

   FLOAT
   wait 1 sec
   Isolation OPEN
   wait 1 sec
   Isolation CLOSE
   FLOAT 20 sec
   STANDBY 10 sec

   Repeat 2 cycles
   Then OFF and STOP
   ========================================================= */


variables
{
  /* Control message = 0x213 / 531 */
  message DBC1::EnergyMgmtBodyCtrl_4 epas1;

  /* Info message = 0x203 / 515 */
  message DBC1::EnergyMgmtBodyInfo_4 epasInfo1;

  msTimer masterTimer;
  msTimer txTimer;
  msTimer finalStopTimer;

  int masterStep = 0;
  int cycleCount = 0;
}


/* =========================================================
   INITIALIZE CTRL_4
   RAW VALUES FROM WORKING MANUAL IG
   ========================================================= */

void initEPAS()
{
  epas1.EMduleDistrPath_R_Calc3 = 30;
  epas1.IsolSwtchOpen_U_Thres3  = 40;

  epas1.DcdcOutUHi_U_HystThres3 = 0;
  epas1.DcdcOutULo_U_HystThres3 = 0;

  epas1.DcdcAout_U_Rq3           = 13;
  epas1.EMduleHystMn_U_Allw3     = 6;
  epas1.PwBus_U_Rq3              = 13;
  epas1.EMduleHystMx_U_Allw3     = 0;
}


/* =========================================================
   INITIALIZE INFO_4
   Working IG:
   00 00 00 00 00 00 A2 80
   ========================================================= */

void initEPASInfo()
{
  epasInfo1.byte(0) = 0;
  epasInfo1.byte(1) = 0;
  epasInfo1.byte(2) = 0;
  epasInfo1.byte(3) = 0;
  epasInfo1.byte(4) = 0;
  epasInfo1.byte(5) = 0;
  epasInfo1.byte(6) = 162;
  epasInfo1.byte(7) = 128;
}


/* =========================================================
   MODE
   0 = OFF
   1 = STANDBY
   3 = FLOAT
   ========================================================= */

void setMode(int mode)
{
  epas1.EMduleMde_D_Rq3 = mode;
}


/* =========================================================
   ISOLATION
   0 = OPEN
   1 = CLOSE
   ========================================================= */

void setIsolation(int value)
{
  epas1.IsolSwtch_B_Cmd3 = value;
}


/* =========================================================
   SEND BOTH MESSAGES
   ========================================================= */

void sendEPAS()
{
  output(epas1);
  output(epasInfo1);
}


/* =========================================================
   START
   ========================================================= */

on start
{
  masterStep = 0;
  cycleCount = 0;

  initEPAS();
  initEPASInfo();

  /* Initial condition */
  setMode(0);
  setIsolation(1);

  sendEPAS();

  write("======================================");
  write("CAN1 12V EPAS TEST START");
  write("CTRL_4 + INFO_4 ACTIVE");
  write("MODE = OFF");
  write("ISOLATION = CLOSE");
  write("======================================");

  /* Send both messages every 100 ms */
  setTimer(txTimer,100);

  /* OFF for 1 second */
  setTimer(masterTimer,1000);
}


/* =========================================================
   PERIODIC TRANSMISSION
   ========================================================= */

on timer txTimer
{
  sendEPAS();

  setTimer(txTimer,100);
}


/* =========================================================
   MASTER TEST SEQUENCE
   ========================================================= */

on timer masterTimer
{
  /* =============================================
     STEP 0
     OFF -> STANDBY
     ============================================= */

  if(masterStep == 0)
  {
    setMode(1);
    setIsolation(1);

    sendEPAS();

    write("MODE = STANDBY");
    write("ISOLATION = CLOSE");
    write("WAIT 2 SEC");

    masterStep = 1;

    setTimer(masterTimer,2000);
  }


  /* =============================================
     STEP 1
     STANDBY -> FLOAT
     ============================================= */

  else if(masterStep == 1)
  {
    setMode(3);
    setIsolation(1);

    sendEPAS();

    write("--------------------------------------");
    write("CYCLE %d OF 2",cycleCount + 1);
    write("MODE = FLOAT");
    write("ISOLATION = CLOSE");
    write("WAIT 1 SEC BEFORE OPEN");

    masterStep = 2;

    setTimer(masterTimer,1000);
  }


  /* =============================================
     STEP 2
     FLOAT remains FLOAT
     Isolation OPEN
     ============================================= */

  else if(masterStep == 2)
  {
    /* MODE IS NOT CHANGED */

    setIsolation(0);

    sendEPAS();

    write("MODE = FLOAT");
    write("ISOLATION = OPEN");
    write("WAIT 1 SEC");

    masterStep = 3;

    setTimer(masterTimer,1000);
  }


  /* =============================================
     STEP 3
     Isolation CLOSE
     FLOAT remains FLOAT
     ============================================= */

  else if(masterStep == 3)
  {
    /* MODE IS NOT CHANGED */

    setIsolation(1);

    sendEPAS();

    write("MODE = FLOAT");
    write("ISOLATION = CLOSE");
    write("FLOAT FOR 20 SEC");

    masterStep = 4;

    setTimer(masterTimer,20000);
  }


  /* =============================================
     STEP 4
     FLOAT -> STANDBY
     ============================================= */

  else if(masterStep == 4)
  {
    setMode(1);
    setIsolation(1);

    sendEPAS();

    write("MODE = STANDBY");
    write("ISOLATION = CLOSE");
    write("WAIT 10 SEC");

    masterStep = 5;

    setTimer(masterTimer,10000);
  }


  /* =============================================
     STEP 5
     CYCLE COMPLETE
     ============================================= */

  else if(masterStep == 5)
  {
    cycleCount++;

    write("--------------------------------------");
    write("CYCLE %d COMPLETE",cycleCount);


    /* ===========================================
       BOTH CYCLES FINISHED
       =========================================== */

    if(cycleCount >= 2)
    {
      setMode(0);
      setIsolation(1);

      sendEPAS();

      write("======================================");
      write("2 CYCLES COMPLETE");
      write("MODE = OFF");
      write("ISOLATION = CLOSE");
      write("WAIT 1 SEC THEN STOP");
      write("======================================");

      setTimer(finalStopTimer,1000);
    }


    /* ===========================================
       START SECOND CYCLE
       =========================================== */

    else
    {
      setMode(3);
      setIsolation(1);

      sendEPAS();

      write("--------------------------------------");
      write("CYCLE %d OF 2",cycleCount + 1);
      write("MODE = FLOAT");
      write("ISOLATION = CLOSE");
      write("WAIT 1 SEC BEFORE OPEN");

      masterStep = 2;

      setTimer(masterTimer,1000);
    }
  }
}


/* =========================================================
   FINAL STOP
   ========================================================= */

on timer finalStopTimer
{
  setMode(0);
  setIsolation(1);

  sendEPAS();

  cancelTimer(txTimer);
  cancelTimer(masterTimer);

  write("======================================");
  write("TEST COMPLETE");
  write("FINAL MODE = OFF");
  write("FINAL ISOLATION = CLOSE");
  write("STOPPING MEASUREMENT");
  write("======================================");

  stop();
}