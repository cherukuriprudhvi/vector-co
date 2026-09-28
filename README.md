

/* =========================================================
   12V EPAS - 2 CYCLE VALIDATION TEST

   SYSTEM SELECTION:
   0 = NONE
   1 = EBB
   2 = EMB
   3 = 48V EPAS
   4 = 12V EPAS

   IMPORTANT:
   EPAS Ctrl_4 initialization values are included.

   SEQUENCE:
   OFF       1 sec
   STANDBY   2 sec

   CYCLE:
   FLOAT
   wait 1 sec
   Isolation OPEN
   wait 1 sec
   Isolation CLOSE
   remain FLOAT 20 sec
   STANDBY 10 sec

   Repeat 2 cycles

   FINAL:
   OFF 1 sec
   Stop measurement
   ========================================================= */


variables
{
  /* ==========================================
     CHANGE THESE FOR YOUR CONNECTED CHANNELS

     For this validation use 4 for channels
     containing 12V EPAS.
     ========================================== */

  int sys1 = 0;
  int sys2 = 0;
  int sys3 = 0;
  int sys4 = 0;
  int sys5 = 0;
  int sys6 = 0;


  msTimer masterTimer;
  msTimer txTimer;
  msTimer finalStopTimer;

  int masterStep = 0;
  int cycleCount = 0;


  /* CAN1 */

  message DBC1::EnergyMgmtBodyCtrl_1 ebb1;
  message DBC1::EnergyMgmtBodyCtrl_2 emb1;
  message DBC1::EnergyMgmtBodyCtrl_3 v481;
  message DBC1::EnergyMgmtBodyCtrl_4 epas1;


  /* CAN2 */

  message DBC2::EnergyMgmtBodyCtrl_1 ebb2;
  message DBC2::EnergyMgmtBodyCtrl_2 emb2;
  message DBC2::EnergyMgmtBodyCtrl_3 v482;
  message DBC2::EnergyMgmtBodyCtrl_4 epas2;


  /* CAN3 */

  message DBC3::EnergyMgmtBodyCtrl_1 ebb3;
  message DBC3::EnergyMgmtBodyCtrl_2 emb3;
  message DBC3::EnergyMgmtBodyCtrl_3 v483;
  message DBC3::EnergyMgmtBodyCtrl_4 epas3;


  /* CAN4 */

  message DBC4::EnergyMgmtBodyCtrl_1 ebb4;
  message DBC4::EnergyMgmtBodyCtrl_2 emb4;
  message DBC4::EnergyMgmtBodyCtrl_3 v484;
  message DBC4::EnergyMgmtBodyCtrl_4 epas4;


  /* CAN5 */

  message DBC5::EnergyMgmtBodyCtrl_1 ebb5;
  message DBC5::EnergyMgmtBodyCtrl_2 emb5;
  message DBC5::EnergyMgmtBodyCtrl_3 v485;
  message DBC5::EnergyMgmtBodyCtrl_4 epas5;


  /* CAN6 */

  message DBC6::EnergyMgmtBodyCtrl_1 ebb6;
  message DBC6::EnergyMgmtBodyCtrl_2 emb6;
  message DBC6::EnergyMgmtBodyCtrl_3 v486;
  message DBC6::EnergyMgmtBodyCtrl_4 epas6;
}


/* =========================================================
   INITIALIZE 12V EPAS CONTROL MESSAGE

   These values came from the working manual Ctrl_4 frame.
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

  epas2.EMduleDistrPath_R_Calc3 = 30;
  epas2.IsolSwtchOpen_U_Thres3  = 40;
  epas2.DcdcOutUHi_U_HystThres3 = 0;
  epas2.DcdcOutULo_U_HystThres3 = 0;
  epas2.DcdcAout_U_Rq3           = 13;
  epas2.EMduleHystMn_U_Allw3     = 6;
  epas2.PwBus_U_Rq3              = 13;
  epas2.EMduleHystMx_U_Allw3     = 0;

  epas3.EMduleDistrPath_R_Calc3 = 30;
  epas3.IsolSwtchOpen_U_Thres3  = 40;
  epas3.DcdcOutUHi_U_HystThres3 = 0;
  epas3.DcdcOutULo_U_HystThres3 = 0;
  epas3.DcdcAout_U_Rq3           = 13;
  epas3.EMduleHystMn_U_Allw3     = 6;
  epas3.PwBus_U_Rq3              = 13;
  epas3.EMduleHystMx_U_Allw3     = 0;

  epas4.EMduleDistrPath_R_Calc3 = 30;
  epas4.IsolSwtchOpen_U_Thres3  = 40;
  epas4.DcdcOutUHi_U_HystThres3 = 0;
  epas4.DcdcOutULo_U_HystThres3 = 0;
  epas4.DcdcAout_U_Rq3           = 13;
  epas4.EMduleHystMn_U_Allw3     = 6;
  epas4.PwBus_U_Rq3              = 13;
  epas4.EMduleHystMx_U_Allw3     = 0;

  epas5.EMduleDistrPath_R_Calc3 = 30;
  epas5.IsolSwtchOpen_U_Thres3  = 40;
  epas5.DcdcOutUHi_U_HystThres3 = 0;
  epas5.DcdcOutULo_U_HystThres3 = 0;
  epas5.DcdcAout_U_Rq3           = 13;
  epas5.EMduleHystMn_U_Allw3     = 6;
  epas5.PwBus_U_Rq3              = 13;
  epas5.EMduleHystMx_U_Allw3     = 0;

  epas6.EMduleDistrPath_R_Calc3 = 30;
  epas6.IsolSwtchOpen_U_Thres3  = 40;
  epas6.DcdcOutUHi_U_HystThres3 = 0;
  epas6.DcdcOutULo_U_HystThres3 = 0;
  epas6.DcdcAout_U_Rq3           = 13;
  epas6.EMduleHystMn_U_Allw3     = 6;
  epas6.PwBus_U_Rq3              = 13;
  epas6.EMduleHystMx_U_Allw3     = 0;
}


/* =========================================================
   START
   ========================================================= */

on start
{
  cycleCount = 0;
  masterStep = 0;

  /* IMPORTANT */
  initEPAS();

  write("========================================");
  write("2-CYCLE EPAS VALIDATION STARTED");
  write("========================================");

  setAllMode(0);
  closeAllIsolation();
  sendAll();

  write("MODE = OFF");
  write("OFF FOR 1 SECOND");

  setTimer(txTimer,100);
  setTimer(masterTimer,1000);
}


/* =========================================================
   TRANSMIT EVERY 100 ms
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
  /* OFF -> STANDBY */

  if(masterStep == 0)
  {
    setAllMode(1);
    closeAllIsolation();
    sendAll();

    write("MODE = STANDBY");
    write("STANDBY FOR 2 SECONDS");

    masterStep = 1;
    setTimer(masterTimer,2000);
  }


  /* STANDBY -> FLOAT */

  else if(masterStep == 1)
  {
    setAllMode(3);
    closeAllIsolation();
    sendAll();

    write("----------------------------------------");
    write("CYCLE %d OF 2",cycleCount + 1);
    write("MODE = FLOAT");
    write("ISOLATION STILL CLOSED");
    write("WAIT 1 SECOND");

    masterStep = 2;
    setTimer(masterTimer,1000);
  }


  /* FLOAT 1 sec -> OPEN */

  else if(masterStep == 2)
  {
    openAllIsolation();
    sendAll();

    write("ISOLATION = OPEN");
    write("WAIT 1 SECOND");

    masterStep = 3;
    setTimer(masterTimer,1000);
  }


  /* OPEN 1 sec -> CLOSE */

  else if(masterStep == 3)
  {
    closeAllIsolation();
    sendAll();

    write("ISOLATION = CLOSE");
    write("MODE REMAINS FLOAT");
    write("FLOAT FOR 20 SECONDS");

    masterStep = 4;
    setTimer(masterTimer,20000);
  }


  /* FLOAT -> STANDBY */

  else if(masterStep == 4)
  {
    setAllMode(1);
    closeAllIsolation();
    sendAll();

    write("MODE = STANDBY");
    write("STANDBY FOR 10 SECONDS");

    masterStep = 5;
    setTimer(masterTimer,10000);
  }


  /* CYCLE COMPLETE */

  else if(masterStep == 5)
  {
    cycleCount++;

    write("========================================");
    write("CYCLE %d OF 2 COMPLETE",cycleCount);
    write("========================================");


    /* BOTH CYCLES FINISHED */

    if(cycleCount >= 2)
    {
      setAllMode(0);
      closeAllIsolation();
      sendAll();

      write("MODE = OFF");
      write("FINAL OFF FOR 1 SECOND");

      setTimer(finalStopTimer,1000);
    }


    /* START SECOND CYCLE */

    else
    {
      setAllMode(3);
      closeAllIsolation();
      sendAll();

      write("----------------------------------------");
      write("CYCLE %d OF 2",cycleCount + 1);
      write("MODE = FLOAT");
      write("ISOLATION STILL CLOSED");
      write("WAIT 1 SECOND");

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
  setAllMode(0);
  closeAllIsolation();
  sendAll();

  cancelTimer(txTimer);
  cancelTimer(masterTimer);

  write("========================================");
  write("TEST COMPLETE");
  write("ALL ACTIVE SYSTEMS OFF");
  write("STOPPING MEASUREMENT");
  write("========================================");

  stop();
}


/* =========================================================
   ALL MODES
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
   ALL ISOLATION OPEN
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
   ALL ISOLATION CLOSE
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
  if(sys1==1) ebb1.EMduleMde_D_Rq=v;
  else if(sys1==2) emb1.EMduleMde_D_Rq2=v;
  else if(sys1==3) v481.UCapMduleMde_D_Rq=v;
  else if(sys1==4) epas1.EMduleMde_D_Rq3=v;
}

void mode2(int v)
{
  if(sys2==1) ebb2.EMduleMde_D_Rq=v;
  else if(sys2==2) emb2.EMduleMde_D_Rq2=v;
  else if(sys2==3) v482.UCapMduleMde_D_Rq=v;
  else if(sys2==4) epas2.EMduleMde_D_Rq3=v;
}

void mode3(int v)
{
  if(sys3==1) ebb3.EMduleMde_D_Rq=v;
  else if(sys3==2) emb3.EMduleMde_D_Rq2=v;
  else if(sys3==3) v483.UCapMduleMde_D_Rq=v;
  else if(sys3==4) epas3.EMduleMde_D_Rq3=v;
}

void mode4(int v)
{
  if(sys4==1) ebb4.EMduleMde_D_Rq=v;
  else if(sys4==2) emb4.EMduleMde_D_Rq2=v;
  else if(sys4==3) v484.UCapMduleMde_D_Rq=v;
  else if(sys4==4) epas4.EMduleMde_D_Rq3=v;
}

void mode5(int v)
{
  if(sys5==1) ebb5.EMduleMde_D_Rq=v;
  else if(sys5==2) emb5.EMduleMde_D_Rq2=v;
  else if(sys5==3) v485.UCapMduleMde_D_Rq=v;
  else if(sys5==4) epas5.EMduleMde_D_Rq3=v;
}

void mode6(int v)
{
  if(sys6==1) ebb6.EMduleMde_D_Rq=v;
  else if(sys6==2) emb6.EMduleMde_D_Rq2=v;
  else if(sys6==3) v486.UCapMduleMde_D_Rq=v;
  else if(sys6==4) epas6.EMduleMde_D_Rq3=v;
}


/* =========================================================
   ISOLATION FUNCTIONS
   0 = OPEN
   1 = CLOSE
   ========================================================= */

void isolation1(int v)
{
  if(sys1==1) ebb1.IsolSwtch_B_Cmd=v;
  else if(sys1==2) emb1.IsolSwtch_B_Cmd2=v;
  else if(sys1==4) epas1.IsolSwtch_B_Cmd3=v;
}

void isolation2(int v)
{
  if(sys2==1) ebb2.IsolSwtch_B_Cmd=v;
  else if(sys2==2) emb2.IsolSwtch_B_Cmd2=v;
  else if(sys2==4) epas2.IsolSwtch_B_Cmd3=v;
}

void isolation3(int v)
{
  if(sys3==1) ebb3.IsolSwtch_B_Cmd=v;
  else if(sys3==2) emb3.IsolSwtch_B_Cmd2=v;
  else if(sys3==4) epas3.IsolSwtch_B_Cmd3=v;
}

void isolation4(int v)
{
  if(sys4==1) ebb4.IsolSwtch_B_Cmd=v;
  else if(sys4==2) emb4.IsolSwtch_B_Cmd2=v;
  else if(sys4==4) epas4.IsolSwtch_B_Cmd3=v;
}

void isolation5(int v)
{
  if(sys5==1) ebb5.IsolSwtch_B_Cmd=v;
  else if(sys5==2) emb5.IsolSwtch_B_Cmd2=v;
  else if(sys5==4) epas5.IsolSwtch_B_Cmd3=v;
}

void isolation6(int v)
{
  if(sys6==1) ebb6.IsolSwtch_B_Cmd=v;
  else if(sys6==2) emb6.IsolSwtch_B_Cmd2=v;
  else if(sys6==4) epas6.IsolSwtch_B_Cmd3=v;
}


/* =========================================================
   SEND ALL
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
   SEND FUNCTIONS
   ========================================================= */

void send1()
{
  if(sys1==1) output(ebb1);
  else if(sys1==2) output(emb1);
  else if(sys1==3) output(v481);
  else if(sys1==4) output(epas1);
}

void send2()
{
  if(sys2==1) output(ebb2);
  else if(sys2==2) output(emb2);
  else if(sys2==3) output(v482);
  else if(sys2==4) output(epas2);
}

void send3()
{
  if(sys3==1) output(ebb3);
  else if(sys3==2) output(emb3);
  else if(sys3==3) output(v483);
  else if(sys3==4) output(epas3);
}

void send4()
{
  if(sys4==1) output(ebb4);
  else if(sys4==2) output(emb4);
  else if(sys4==3) output(v484);
  else if(sys4==4) output(epas4);
}

void send5()
{
  if(sys5==1) output(ebb5);
  else if(sys5==2) output(emb5);
  else if(sys5==3) output(v485);
  else if(sys5==4) output(epas5);
}

void send6()
{
  if(sys6==1) output(ebb6);
  else if(sys6==2) output(emb6);
  else if(sys6==3) output(v486);
  else if(sys6==4) output(epas6);
}