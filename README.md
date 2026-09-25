

/* =========================================================
   FINAL 5-DAY / 120-HOUR MASTER

   MANUAL SYSTEM SELECTION:
   0 = NOTHING CONNECTED
   1 = EBB
   2 = EMB
   3 = 48V EPAS
   4 = 12V EPAS

   CAN1 -> DBC1
   CAN2 -> DBC2
   CAN3 -> DBC3
   CAN4 -> DBC4
   CAN5 -> DBC5
   CAN6 -> DBC6

   STARTUP - ONCE ONLY:
   OFF       1 sec
   STANDBY   2 sec
   FLOAT
   ISOLATION OPEN  1 sec
   ISOLATION CLOSE

   EACH 24-HOUR CYCLE:
   FLOAT     18 hours
   STANDBY    6 hours

   On every transition STANDBY -> FLOAT:
   FLOAT
   ISOLATION OPEN 1 sec
   ISOLATION CLOSE
   FLOAT 18 hours

   Repeat 5 cycles = 120 hours.

   48V EPAS:
   NO isolation OPEN/CLOSE.

   END:
   Final 6-hour STANDBY completes
   -> ALL ACTIVE SYSTEMS OFF
   -> wait 2 sec transmitting OFF
   -> stop measurement
   ========================================================= */


variables
{
  /* =====================================================
     EDIT ONLY THESE SIX VALUES BEFORE THE REAL TEST

     0=None
     1=EBB
     2=EMB
     3=48V EPAS
     4=12V EPAS
     ===================================================== */

  int sys1 = 0;     // CAN1
  int sys2 = 0;     // CAN2
  int sys3 = 0;     // CAN3
  int sys4 = 0;     // CAN4
  int sys5 = 0;     // CAN5
  int sys6 = 0;     // CAN6


  /* ===== MASTER TIMERS ===== */

  msTimer masterTimer;
  msTimer txTimer;
  msTimer finalStopTimer;


  /* ===== STATE =====

     0 = Initial OFF
     1 = Initial STANDBY
     2 = Initial Isolation OPEN
     3 = FLOAT 18 hours
     4 = STANDBY 6 hours
     5 = Cycle Isolation OPEN
     6 = FINAL OFF
  */

  int masterStep = 0;

  /* Completed 24-hour cycles */
  int cycleCount = 0;


  /* =====================================================
     CAN1 / DBC1
     ===================================================== */

  message DBC1::EnergyMgmtBodyCtrl_1 ebb1;
  message DBC1::EnergyMgmtBodyCtrl_2 emb1;
  message DBC1::EnergyMgmtBodyCtrl_3 v481;
  message DBC1::EnergyMgmtBodyCtrl_4 epas1;


  /* =====================================================
     CAN2 / DBC2
     ===================================================== */

  message DBC2::EnergyMgmtBodyCtrl_1 ebb2;
  message DBC2::EnergyMgmtBodyCtrl_2 emb2;
  message DBC2::EnergyMgmtBodyCtrl_3 v482;
  message DBC2::EnergyMgmtBodyCtrl_4 epas2;


  /* =====================================================
     CAN3 / DBC3
     ===================================================== */

  message DBC3::EnergyMgmtBodyCtrl_1 ebb3;
  message DBC3::EnergyMgmtBodyCtrl_2 emb3;
  message DBC3::EnergyMgmtBodyCtrl_3 v483;
  message DBC3::EnergyMgmtBodyCtrl_4 epas3;


  /* =====================================================
     CAN4 / DBC4
     ===================================================== */

  message DBC4::EnergyMgmtBodyCtrl_1 ebb4;
  message DBC4::EnergyMgmtBodyCtrl_2 emb4;
  message DBC4::EnergyMgmtBodyCtrl_3 v484;
  message DBC4::EnergyMgmtBodyCtrl_4 epas4;


  /* =====================================================
     CAN5 / DBC5
     ===================================================== */

  message DBC5::EnergyMgmtBodyCtrl_1 ebb5;
  message DBC5::EnergyMgmtBodyCtrl_2 emb5;
  message DBC5::EnergyMgmtBodyCtrl_3 v485;
  message DBC5::EnergyMgmtBodyCtrl_4 epas5;


  /* =====================================================
     CAN6 / DBC6
     ===================================================== */

  message DBC6::EnergyMgmtBodyCtrl_1 ebb6;
  message DBC6::EnergyMgmtBodyCtrl_2 emb6;
  message DBC6::EnergyMgmtBodyCtrl_3 v486;
  message DBC6::EnergyMgmtBodyCtrl_4 epas6;
}


/* =========================================================
   START
   ========================================================= */

on start
{
  cycleCount = 0;
  masterStep = 0;

  write("==============================================");
  write("FINAL 5-DAY MASTER STARTED");
  write("TARGET = 5 x 24 HOURS = 120 HOURS");
  write("==============================================");

  printSelection(1,sys1);
  printSelection(2,sys2);
  printSelection(3,sys3);
  printSelection(4,sys4);
  printSelection(5,sys5);
  printSelection(6,sys6);


  /* Initial state:
     ALL active systems OFF
     Isolation CLOSED where applicable */

  setAllMode(0);
  closeAllIsolation();

  sendAll();

  write("ALL ACTIVE SYSTEMS: OFF");
  write("INITIAL OFF: 1 SECOND");

  /* Keep control messages transmitting */
  setTimer(txTimer,100);

  /* OFF for 1 second */
  setTimer(masterTimer,1000);
}


/* =========================================================
   DISPLAY SYSTEM SELECTION
   ========================================================= */

void printSelection(int ch, int sys)
{
  if(sys == 0)
    write("CAN%d: NOT USED",ch);

  else if(sys == 1)
    write("CAN%d: EBB",ch);

  else if(sys == 2)
    write("CAN%d: EMB",ch);

  else if(sys == 3)
    write("CAN%d: 48V EPAS",ch);

  else if(sys == 4)
    write("CAN%d: 12V EPAS",ch);

  else
    write("CAN%d: INVALID SELECTION",ch);
}


/* =========================================================
   100 ms CYCLIC TRANSMISSION

   Runs for entire 5-day test.
   ========================================================= */

on timer txTimer
{
  sendAll();

  setTimer(txTimer,100);
}


/* =========================================================
   MASTER SEQUENCE
   ========================================================= */

on timer masterTimer
{
  /* -----------------------------------------------------
     STEP 0

     Initial OFF finished.
     Enter STANDBY for 2 seconds.
     ----------------------------------------------------- */

  if(masterStep == 0)
  {
    setAllMode(1);

    write("ALL ACTIVE SYSTEMS: STANDBY");
    write("INITIAL STANDBY: 2 SECONDS");

    masterStep = 1;

    setTimer(masterTimer,2000);
  }


  /* -----------------------------------------------------
     STEP 1

     Initial STANDBY finished.

     Enter FLOAT.
     Open isolation immediately for systems that have it.
     Keep OPEN for 1 second.

     48V remains FLOAT and skips isolation.
     ----------------------------------------------------- */

  else if(masterStep == 1)
  {
    setAllMode(3);

    openAllIsolation();

    write("ALL ACTIVE SYSTEMS: FLOAT");
    write("EBB / EMB / 12V EPAS: ISOLATION OPEN");
    write("48V EPAS: ISOLATION SKIPPED");

    masterStep = 2;

    setTimer(masterTimer,1000);
  }


  /* -----------------------------------------------------
     STEP 2

     Initial isolation has been OPEN for 1 second.
     CLOSE isolation.

     Start first 18-hour FLOAT period.
     ----------------------------------------------------- */

  else if(masterStep == 2)
  {
    closeAllIsolation();

    write("ISOLATION CLOSE");
    write("CYCLE 1: FLOAT 18 HOURS STARTED");

    masterStep = 3;

    setTimer(masterTimer,64800000);
  }


  /* -----------------------------------------------------
     STEP 3

     18-hour FLOAT finished.
     Enter STANDBY for 6 hours.
     ----------------------------------------------------- */

  else if(masterStep == 3)
  {
    setAllMode(1);

    write("FLOAT 18 HOURS COMPLETE");
    write("STANDBY 6 HOURS STARTED");

    masterStep = 4;

    setTimer(masterTimer,21600000);
  }


  /* -----------------------------------------------------
     STEP 4

     6-hour STANDBY finished.
     One complete 24-hour cycle is now finished.
     ----------------------------------------------------- */

  else if(masterStep == 4)
  {
    cycleCount++;

    write("==============================================");
    write("24-HOUR CYCLE %d COMPLETE",cycleCount);
    write("==============================================");


    /* Five complete cycles = 120 hours */

    if(cycleCount >= 5)
    {
      write("ALL 5 CYCLES COMPLETE");
      write("COMMANDING FINAL OFF");

      setAllMode(0);
      closeAllIsolation();

      sendAll();

      masterStep = 6;

      /*
         Keep OFF transmitting for 2 seconds
         before stopping measurement.
      */

      setTimer(finalStopTimer,2000);
    }


    /* Otherwise begin next FLOAT cycle */

    else
    {
      setAllMode(3);

      openAllIsolation();

      write("CYCLE %d STARTING",cycleCount + 1);
      write("ALL ACTIVE SYSTEMS: FLOAT");
      write("ISOLATION OPEN FOR 1 SECOND");
      write("48V EPAS: ISOLATION SKIPPED");

      masterStep = 5;

      setTimer(masterTimer,1000);
    }
  }


  /* -----------------------------------------------------
     STEP 5

     Isolation OPEN for 1 second during transition
     into the next FLOAT cycle.

     CLOSE isolation and remain FLOAT 18 hours.
     ----------------------------------------------------- */

  else if(masterStep == 5)
  {
    closeAllIsolation();

    write("ISOLATION CLOSE");
    write("CYCLE %d: FLOAT 18 HOURS STARTED",
          cycleCount + 1);

    masterStep = 3;

    setTimer(masterTimer,64800000);
  }
}


/* =========================================================
   FINAL AUTOMATIC SHUTDOWN
   ========================================================= */

on timer finalStopTimer
{
  /*
     OFF has been transmitted cyclically for
     approximately 2 seconds before reaching here.
  */

  setAllMode(0);
  closeAllIsolation();

  sendAll();

  cancelTimer(txTimer);
  cancelTimer(masterTimer);

  write("==============================================");
  write("5-DAY TEST COMPLETE");
  write("ALL ACTIVE SYSTEMS = OFF");
  write("ISOLATION = CLOSED WHERE APPLICABLE");
  write("STOPPING CANALYZER MEASUREMENT");
  write("==============================================");

  stop();
}


/* =========================================================
   SET ALL ACTIVE SYSTEMS TO SAME MODE
   ========================================================= */

void setAllMode(int v)
{
  mode1(v);
  mode2(v);
  mode3(v);
  mode4(v);
  mode5(v);
  mode6(v);
}


/* =========================================================
   ISOLATION OPEN
   48V IS AUTOMATICALLY SKIPPED
   ========================================================= */

void openAllIsolation()
{
  isolation1(0);
  isolation2(0);
  isolation3(0);
  isolation4(0);
  isolation5(0);
  isolation6(0);
}


/* =========================================================
   ISOLATION CLOSE
   48V IS AUTOMATICALLY SKIPPED
   ========================================================= */

void closeAllIsolation()
{
  isolation1(1);
  isolation2(1);
  isolation3(1);
  isolation4(1);
  isolation5(1);
  isolation6(1);
}


/* =========================================================
   MODE FUNCTIONS
   ========================================================= */

void mode1(int v)
{
  if(sys1==1)
    ebb1.EMduleMde_D_Rq=v;

  else if(sys1==2)
    emb1.EMduleMde_D_Rq2=v;

  else if(sys1==3)
    v481.UCapMduleMde_D_Rq=v;

  else if(sys1==4)
    epas1.EMduleMde_D_Rq3=v;
}


void mode2(int v)
{
  if(sys2==1)
    ebb2.EMduleMde_D_Rq=v;

  else if(sys2==2)
    emb2.EMduleMde_D_Rq2=v;

  else if(sys2==3)
    v482.UCapMduleMde_D_Rq=v;

  else if(sys2==4)
    epas2.EMduleMde_D_Rq3=v;
}


void mode3(int v)
{
  if(sys3==1)
    ebb3.EMduleMde_D_Rq=v;

  else if(sys3==2)
    emb3.EMduleMde_D_Rq2=v;

  else if(sys3==3)
    v483.UCapMduleMde_D_Rq=v;

  else if(sys3==4)
    epas3.EMduleMde_D_Rq3=v;
}


void mode4(int v)
{
  if(sys4==1)
    ebb4.EMduleMde_D_Rq=v;

  else if(sys4==2)
    emb4.EMduleMde_D_Rq2=v;

  else if(sys4==3)
    v484.UCapMduleMde_D_Rq=v;

  else if(sys4==4)
    epas4.EMduleMde_D_Rq3=v;
}


void mode5(int v)
{
  if(sys5==1)
    ebb5.EMduleMde_D_Rq=v;

  else if(sys5==2)
    emb5.EMduleMde_D_Rq2=v;

  else if(sys5==3)
    v485.UCapMduleMde_D_Rq=v;

  else if(sys5==4)
    epas5.EMduleMde_D_Rq3=v;
}


void mode6(int v)
{
  if(sys6==1)
    ebb6.EMduleMde_D_Rq=v;

  else if(sys6==2)
    emb6.EMduleMde_D_Rq2=v;

  else if(sys6==3)
    v486.UCapMduleMde_D_Rq=v;

  else if(sys6==4)
    epas6.EMduleMde_D_Rq3=v;
}


/* =========================================================
   ISOLATION FUNCTIONS

   0 = OPEN
   1 = CLOSE

   48V EPAS (sys == 3) has no isolation,
   therefore no action occurs.
   ========================================================= */

void isolation1(int v)
{
  if(sys1==1)
    ebb1.IsolSwtch_B_Cmd=v;

  else if(sys1==2)
    emb1.IsolSwtch_B_Cmd2=v;

  else if(sys1==4)
    epas1.IsolSwtch_B_Cmd3=v;
}


void isolation2(int v)
{
  if(sys2==1)
    ebb2.IsolSwtch_B_Cmd=v;

  else if(sys2==2)
    emb2.IsolSwtch_B_Cmd2=v;

  else if(sys2==4)
    epas2.IsolSwtch_B_Cmd3=v;
}


void isolation3(int v)
{
  if(sys3==1)
    ebb3.IsolSwtch_B_Cmd=v;

  else if(sys3==2)
    emb3.IsolSwtch_B_Cmd2=v;

  else if(sys3==4)
    epas3.IsolSwtch_B_Cmd3=v;
}


void isolation4(int v)
{
  if(sys4==1)
    ebb4.IsolSwtch_B_Cmd=v;

  else if(sys4==2)
    emb4.IsolSwtch_B_Cmd2=v;

  else if(sys4==4)
    epas4.IsolSwtch_B_Cmd3=v;
}


void isolation5(int v)
{
  if(sys5==1)
    ebb5.IsolSwtch_B_Cmd=v;

  else if(sys5==2)
    emb5.IsolSwtch_B_Cmd2=v;

  else if(sys5==4)
    epas5.IsolSwtch_B_Cmd3=v;
}


void isolation6(int v)
{
  if(sys6==1)
    ebb6.IsolSwtch_B_Cmd=v;

  else if(sys6==2)
    emb6.IsolSwtch_B_Cmd2=v;

  else if(sys6==4)
    epas6.IsolSwtch_B_Cmd3=v;
}


/* =========================================================
   SEND ALL ACTIVE CHANNELS
   ========================================================= */

void sendAll()
{
  send1();
  send2();
  send3();
  send4();
  send5();
  send6();
}


/* =========================================================
   SEND CORRECT CONTROL MESSAGE
   ========================================================= */

void send1()
{
  if(sys1==1)
    output(ebb1);

  else if(sys1==2)
    output(emb1);

  else if(sys1==3)
    output(v481);

  else if(sys1==4)
    output(epas1);
}


void send2()
{
  if(sys2==1)
    output(ebb2);

  else if(sys2==2)
    output(emb2);

  else if(sys2==3)
    output(v482);

  else if(sys2==4)
    output(epas2);
}


void send3()
{
  if(sys3==1)
    output(ebb3);

  else if(sys3==2)
    output(emb3);

  else if(sys3==3)
    output(v483);

  else if(sys3==4)
    output(epas3);
}


void send4()
{
  if(sys4==1)
    output(ebb4);

  else if(sys4==2)
    output(emb4);

  else if(sys4==3)
    output(v484);

  else if(sys4==4)
    output(epas4);
}


void send5()
{
  if(sys5==1)
    output(ebb5);

  else if(sys5==2)
    output(emb5);

  else if(sys5==3)
    output(v485);

  else if(sys5==4)
    output(epas5);
}


void send6()
{
  if(sys6==1)
    output(ebb6);

  else if(sys6==2)
    output(emb6);

  else if(sys6==3)
    output(v486);

  else if(sys6==4)
    output(epas6);
}