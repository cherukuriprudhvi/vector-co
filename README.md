
/* =========================================================
   ACCELERATED 5-CYCLE TEST MASTER

   SYSTEM:
   0 = NONE
   1 = EBB
   2 = EMB
   3 = 48V EPAS
   4 = 12V EPAS

   TEST SEQUENCE:

   START ONCE:
   OFF       = 1 second
   STANDBY   = 2 seconds
   FLOAT
   Isolation OPEN = 1 second
   Isolation CLOSE

   EACH TEST CYCLE:
   FLOAT     = 20 seconds
   STANDBY   = 10 seconds

   REPEAT = 5 cycles

   After Cycle 5:
   OFF
   Wait 2 seconds
   Stop CANalyzer measurement automatically

   48V EPAS skips isolation.
   ========================================================= */


variables
{
  /* =====================================================
     CHANGE ONLY THESE SIX VALUES

     0 = NONE
     1 = EBB
     2 = EMB
     3 = 48V EPAS
     4 = 12V EPAS
     ===================================================== */

  int sys1 = 0;     // CAN1
  int sys2 = 0;     // CAN2
  int sys3 = 0;     // CAN3
  int sys4 = 0;     // CAN4
  int sys5 = 0;     // CAN5
  int sys6 = 0;     // CAN6


  /* MASTER TIMERS */

  msTimer masterTimer;
  msTimer txTimer;
  msTimer finalStopTimer;


  /*
     MASTER STATES

     0 = Initial OFF
     1 = Initial STANDBY
     2 = Initial Isolation OPEN
     3 = FLOAT
     4 = STANDBY
     5 = Next-cycle Isolation OPEN
     6 = Final OFF
  */

  int masterStep = 0;

  int cycleCount = 0;


  /* ==========================
     CAN1 / DBC1
     ========================== */

  message DBC1::EnergyMgmtBodyCtrl_1 ebb1;
  message DBC1::EnergyMgmtBodyCtrl_2 emb1;
  message DBC1::EnergyMgmtBodyCtrl_3 v481;
  message DBC1::EnergyMgmtBodyCtrl_4 epas1;


  /* ==========================
     CAN2 / DBC2
     ========================== */

  message DBC2::EnergyMgmtBodyCtrl_1 ebb2;
  message DBC2::EnergyMgmtBodyCtrl_2 emb2;
  message DBC2::EnergyMgmtBodyCtrl_3 v482;
  message DBC2::EnergyMgmtBodyCtrl_4 epas2;


  /* ==========================
     CAN3 / DBC3
     ========================== */

  message DBC3::EnergyMgmtBodyCtrl_1 ebb3;
  message DBC3::EnergyMgmtBodyCtrl_2 emb3;
  message DBC3::EnergyMgmtBodyCtrl_3 v483;
  message DBC3::EnergyMgmtBodyCtrl_4 epas3;


  /* ==========================
     CAN4 / DBC4
     ========================== */

  message DBC4::EnergyMgmtBodyCtrl_1 ebb4;
  message DBC4::EnergyMgmtBodyCtrl_2 emb4;
  message DBC4::EnergyMgmtBodyCtrl_3 v484;
  message DBC4::EnergyMgmtBodyCtrl_4 epas4;


  /* ==========================
     CAN5 / DBC5
     ========================== */

  message DBC5::EnergyMgmtBodyCtrl_1 ebb5;
  message DBC5::EnergyMgmtBodyCtrl_2 emb5;
  message DBC5::EnergyMgmtBodyCtrl_3 v485;
  message DBC5::EnergyMgmtBodyCtrl_4 epas5;


  /* ==========================
     CAN6 / DBC6
     ========================== */

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
  write("ACCELERATED 5-CYCLE TEST STARTED");
  write("FLOAT = 20 SEC / STANDBY = 10 SEC");
  write("==============================================");

  printSelection(1,sys1);
  printSelection(2,sys2);
  printSelection(3,sys3);
  printSelection(4,sys4);
  printSelection(5,sys5);
  printSelection(6,sys6);


  /* Initial OFF */

  setAllMode(0);

  /* Make sure isolation begins CLOSED */

  closeAllIsolation();

  sendAll();

  write("ALL ACTIVE SYSTEMS: OFF");
  write("OFF FOR 1 SECOND");


  /* Start cyclic transmission every 100 ms */

  setTimer(txTimer,100);


  /* OFF for 1 second */

  setTimer(masterTimer,1000);
}


/* =========================================================
   SHOW SELECTED SYSTEMS
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
   CYCLIC TRANSMISSION - 100 ms
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

  /* =====================================================
     STEP 0
     OFF complete -> STANDBY
     ===================================================== */

  if(masterStep == 0)
  {
    setAllMode(1);

    sendAll();

    write("----------------------------------------------");
    write("ALL ACTIVE SYSTEMS: STANDBY");
    write("STANDBY FOR 2 SECONDS");

    masterStep = 1;

    setTimer(masterTimer,2000);
  }


  /* =====================================================
     STEP 1
     STANDBY complete -> FLOAT
     Isolation OPEN
     ===================================================== */

  else if(masterStep == 1)
  {
    setAllMode(3);

    openAllIsolation();

    sendAll();

    write("----------------------------------------------");
    write("ALL ACTIVE SYSTEMS: FLOAT");
    write("ISOLATION OPEN FOR 1 SECOND");
    write("48V EPAS: ISOLATION SKIPPED");

    masterStep = 2;

    setTimer(masterTimer,1000);
  }


  /* =====================================================
     STEP 2
     Close isolation
     Begin Cycle 1 FLOAT = 20 seconds
     ===================================================== */

  else if(masterStep == 2)
  {
    closeAllIsolation();

    sendAll();

    write("----------------------------------------------");
    write("ISOLATION CLOSE");
    write("CYCLE 1: FLOAT FOR 20 SECONDS");

    masterStep = 3;

    setTimer(masterTimer,20000);
  }


  /* =====================================================
     STEP 3
     FLOAT finished -> STANDBY
     ===================================================== */

  else if(masterStep == 3)
  {
    setAllMode(1);

    sendAll();

    write("----------------------------------------------");
    write("FLOAT COMPLETE");
    write("STANDBY FOR 10 SECONDS");

    masterStep = 4;

    setTimer(masterTimer,10000);
  }


  /* =====================================================
     STEP 4
     STANDBY finished
     Complete one cycle
     ===================================================== */

  else if(masterStep == 4)
  {
    cycleCount++;

    write("==============================================");
    write("CYCLE %d OF 5 COMPLETE",cycleCount);
    write("==============================================");


    /* ===============================================
       ALL 5 CYCLES COMPLETE
       =============================================== */

    if(cycleCount >= 5)
    {
      setAllMode(0);

      closeAllIsolation();

      sendAll();

      write("ALL 5 CYCLES COMPLETE");
      write("ALL ACTIVE SYSTEMS: OFF");
      write("FINAL OFF FOR 2 SECONDS");

      masterStep = 6;

      setTimer(finalStopTimer,2000);
    }


    /* ===============================================
       START NEXT CYCLE
       =============================================== */

    else
    {
      setAllMode(3);

      openAllIsolation();

      sendAll();

      write("----------------------------------------------");
      write("STARTING CYCLE %d",cycleCount + 1);
      write("ALL ACTIVE SYSTEMS: FLOAT");
      write("ISOLATION OPEN FOR 1 SECOND");
      write("48V EPAS: ISOLATION SKIPPED");

      masterStep = 5;

      setTimer(masterTimer,1000);
    }
  }


  /* =====================================================
     STEP 5
     Isolation has been OPEN for 1 sec.
     Close it and stay FLOAT for 20 sec.
     ===================================================== */

  else if(masterStep == 5)
  {
    closeAllIsolation();

    sendAll();

    write("----------------------------------------------");
    write("ISOLATION CLOSE");
    write("CYCLE %d: FLOAT FOR 20 SECONDS",
          cycleCount + 1);

    masterStep = 3;

    setTimer(masterTimer,20000);
  }
}


/* =========================================================
   FINAL AUTOMATIC SHUTDOWN
   ========================================================= */

on timer finalStopTimer
{
  setAllMode(0);

  closeAllIsolation();

  sendAll();

  cancelTimer(txTimer);
  cancelTimer(masterTimer);

  write("==============================================");
  write("ACCELERATED TEST COMPLETE");
  write("5 OF 5 CYCLES COMPLETE");
  write("ALL ACTIVE SYSTEMS = OFF");
  write("ISOLATION = CLOSED WHERE APPLICABLE");
  write("STOPPING CANALYZER MEASUREMENT");
  write("==============================================");

  stop();
}


/* =========================================================
   SET MODE FOR ALL CHANNELS
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
   OPEN ISOLATION
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
   CLOSE ISOLATION
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
   MODE - CAN1
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


/* =========================================================
   MODE - CAN2
   ========================================================= */

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


/* =========================================================
   MODE - CAN3
   ========================================================= */

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


/* =========================================================
   MODE - CAN4
   ========================================================= */

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


/* =========================================================
   MODE - CAN5
   ========================================================= */

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


/* =========================================================
   MODE - CAN6
   ========================================================= */

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
   ISOLATION - CAN1

   48V EPAS automatically does nothing.
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


/* =========================================================
   ISOLATION - CAN2
   ========================================================= */

void isolation2(int v)
{
  if(sys2==1)
    ebb2.IsolSwtch_B_Cmd=v;

  else if(sys2==2)
    emb2.IsolSwtch_B_Cmd2=v;

  else if(sys2==4)
    epas2.IsolSwtch_B_Cmd3=v;
}


/* =========================================================
   ISOLATION - CAN3
   ========================================================= */

void isolation3(int v)
{
  if(sys3==1)
    ebb3.IsolSwtch_B_Cmd=v;

  else if(sys3==2)
    emb3.IsolSwtch_B_Cmd2=v;

  else if(sys3==4)
    epas3.IsolSwtch_B_Cmd3=v;
}


/* =========================================================
   ISOLATION - CAN4
   ========================================================= */

void isolation4(int v)
{
  if(sys4==1)
    ebb4.IsolSwtch_B_Cmd=v;

  else if(sys4==2)
    emb4.IsolSwtch_B_Cmd2=v;

  else if(sys4==4)
    epas4.IsolSwtch_B_Cmd3=v;
}


/* =========================================================
   ISOLATION - CAN5
   ========================================================= */

void isolation5(int v)
{
  if(sys5==1)
    ebb5.IsolSwtch_B_Cmd=v;

  else if(sys5==2)
    emb5.IsolSwtch_B_Cmd2=v;

  else if(sys5==4)
    epas5.IsolSwtch_B_Cmd3=v;
}


/* =========================================================
   ISOLATION - CAN6
   ========================================================= */

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
   SEND CAN1
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


/* =========================================================
   SEND CAN2
   ========================================================= */

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


/* =========================================================
   SEND CAN3
   ========================================================= */

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


/* =========================================================
   SEND CAN4
   ========================================================= */

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


/* =========================================================
   SEND CAN5
   ========================================================= */

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


/* =========================================================
   SEND CAN6
   ========================================================= */

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
