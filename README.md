

variables
{
  /* One sequence timer + Tx timer per channel */
  msTimer seq1, seq2, seq3, seq4, seq5, seq6;
  msTimer tx1,  tx2,  tx3,  tx4,  tx5,  tx6;

  msTimer stopTimer;

  /* 0 Unknown, 1 EBB, 2 EMB, 3 48V, 4 EPAS */
  int sys1 = 0;
  int sys2 = 0;
  int sys3 = 0;
  int sys4 = 0;
  int sys5 = 0;
  int sys6 = 0;

  int step1 = 0;
  int step2 = 0;
  int step3 = 0;
  int step4 = 0;
  int step5 = 0;
  int step6 = 0;

  int cycle1 = 0;
  int cycle2 = 0;
  int cycle3 = 0;
  int cycle4 = 0;
  int cycle5 = 0;
  int cycle6 = 0;

  /* ===== CAN1 / DBC1 ===== */
  message DBC1::EnergyMgmtBodyCtrl_1 ebb1;
  message DBC1::EnergyMgmtBodyCtrl_2 emb1;
  message DBC1::EnergyMgmtBodyCtrl_3 v481;
  message DBC1::EnergyMgmtBodyCtrl_4 epas1;

  /* ===== CAN2 / DBC2 ===== */
  message DBC2::EnergyMgmtBodyCtrl_1 ebb2;
  message DBC2::EnergyMgmtBodyCtrl_2 emb2;
  message DBC2::EnergyMgmtBodyCtrl_3 v482;
  message DBC2::EnergyMgmtBodyCtrl_4 epas2;

  /* ===== CAN3 / DBC3 ===== */
  message DBC3::EnergyMgmtBodyCtrl_1 ebb3;
  message DBC3::EnergyMgmtBodyCtrl_2 emb3;
  message DBC3::EnergyMgmtBodyCtrl_3 v483;
  message DBC3::EnergyMgmtBodyCtrl_4 epas3;

  /* ===== CAN4 / DBC4 ===== */
  message DBC4::EnergyMgmtBodyCtrl_1 ebb4;
  message DBC4::EnergyMgmtBodyCtrl_2 emb4;
  message DBC4::EnergyMgmtBodyCtrl_3 v484;
  message DBC4::EnergyMgmtBodyCtrl_4 epas4;

  /* ===== CAN5 / DBC5 ===== */
  message DBC5::EnergyMgmtBodyCtrl_1 ebb5;
  message DBC5::EnergyMgmtBodyCtrl_2 emb5;
  message DBC5::EnergyMgmtBodyCtrl_3 v485;
  message DBC5::EnergyMgmtBodyCtrl_4 epas5;

  /* ===== CAN6 / DBC6 ===== */
  message DBC6::EnergyMgmtBodyCtrl_1 ebb6;
  message DBC6::EnergyMgmtBodyCtrl_2 emb6;
  message DBC6::EnergyMgmtBodyCtrl_3 v486;
  message DBC6::EnergyMgmtBodyCtrl_4 epas6;
}


/* =========================================================
   DETECTION
   ========================================================= */

on message CAN1.*
{
  if (sys1 != 0) return;
  sys1 = detectSystem(this.id);

  if (sys1 != 0)
  {
    write("CAN1 DETECTED SYSTEM %d", sys1);
    start1();
  }
}

on message CAN2.*
{
  if (sys2 != 0) return;
  sys2 = detectSystem(this.id);

  if (sys2 != 0)
  {
    write("CAN2 DETECTED SYSTEM %d", sys2);
    start2();
  }
}

on message CAN3.*
{
  if (sys3 != 0) return;
  sys3 = detectSystem(this.id);

  if (sys3 != 0)
  {
    write("CAN3 DETECTED SYSTEM %d", sys3);
    start3();
  }
}

on message CAN4.*
{
  if (sys4 != 0) return;
  sys4 = detectSystem(this.id);

  if (sys4 != 0)
  {
    write("CAN4 DETECTED SYSTEM %d", sys4);
    start4();
  }
}

on message CAN5.*
{
  if (sys5 != 0) return;
  sys5 = detectSystem(this.id);

  if (sys5 != 0)
  {
    write("CAN5 DETECTED SYSTEM %d", sys5);
    start5();
  }
}

on message CAN6.*
{
  if (sys6 != 0) return;
  sys6 = detectSystem(this.id);

  if (sys6 != 0)
  {
    write("CAN6 DETECTED SYSTEM %d", sys6);
    start6();
  }
}


/* =========================================================
   SYSTEM DETECTOR

   1 = EBB
   2 = EMB
   3 = 48V EPAS
   4 = EPAS
   ========================================================= */

int detectSystem(long id)
{
  if (id == 273 || id == 304 ||
      id == 544 || id == 560 || id == 1024)
    return 1;

  if (id == 272 || id == 305 ||
      id == 545 || id == 561 ||
      id == 769 || id == 1025)
    return 2;

  if (id == 256 || id == 306 || id == 770)
    return 3;

  if (id == 309 || id == 1026)
    return 4;

  return 0;
}


/* =========================================================
   START EACH CHANNEL
   OFF = 2 seconds
   ========================================================= */

void start1()
{
  cycle1 = 0;
  step1 = 0;
  mode1(0);
  if (sys1 != 3) isolation1(1);
  setTimer(tx1,100);
  setTimer(seq1,2000);
  write("CAN1: OFF");
}

void start2()
{
  cycle2 = 0;
  step2 = 0;
  mode2(0);
  if (sys2 != 3) isolation2(1);
  setTimer(tx2,100);
  setTimer(seq2,2000);
  write("CAN2: OFF");
}

void start3()
{
  cycle3 = 0;
  step3 = 0;
  mode3(0);
  if (sys3 != 3) isolation3(1);
  setTimer(tx3,100);
  setTimer(seq3,2000);
  write("CAN3: OFF");
}

void start4()
{
  cycle4 = 0;
  step4 = 0;
  mode4(0);
  if (sys4 != 3) isolation4(1);
  setTimer(tx4,100);
  setTimer(seq4,2000);
  write("CAN4: OFF");
}

void start5()
{
  cycle5 = 0;
  step5 = 0;
  mode5(0);
  if (sys5 != 3) isolation5(1);
  setTimer(tx5,100);
  setTimer(seq5,2000);
  write("CAN5: OFF");
}

void start6()
{
  cycle6 = 0;
  step6 = 0;
  mode6(0);
  if (sys6 != 3) isolation6(1);
  setTimer(tx6,100);
  setTimer(seq6,2000);
  write("CAN6: OFF");
}


/* =========================================================
   100 ms PERIODIC TRANSMISSION
   ========================================================= */

on timer tx1 { send1(); setTimer(tx1,100); }
on timer tx2 { send2(); setTimer(tx2,100); }
on timer tx3 { send3(); setTimer(tx3,100); }
on timer tx4 { send4(); setTimer(tx4,100); }
on timer tx5 { send5(); setTimer(tx5,100); }
on timer tx6 { send6(); setTimer(tx6,100); }


/* =========================================================
   SHORT TEST SEQUENCES

   OFF       2 sec
   STANDBY   5 sec
   FLOAT     5 sec
   ISO OPEN  1 sec
   ISO CLOSE
   FLOAT     5 sec
   STANDBY   3 sec
   OFF       2 sec

   Repeat 4 cycles.
   ========================================================= */

on timer seq1 { sequence1(); }
on timer seq2 { sequence2(); }
on timer seq3 { sequence3(); }
on timer seq4 { sequence4(); }
on timer seq5 { sequence5(); }
on timer seq6 { sequence6(); }


void sequence1()
{
  if (step1 == 0)
  {
    mode1(1);
    step1 = 1;
    write("CAN1: STANDBY");
    setTimer(seq1,5000);
  }
  else if (step1 == 1)
  {
    mode1(3);
    step1 = 2;
    write("CAN1: FLOAT");
    setTimer(seq1,5000);
  }
  else if (step1 == 2)
  {
    if (sys1 != 3)
    {
      isolation1(0);
      write("CAN1: ISOLATION OPEN");
    }

    step1 = 3;
    setTimer(seq1,1000);
  }
  else if (step1 == 3)
  {
    if (sys1 != 3)
    {
      isolation1(1);
      write("CAN1: ISOLATION CLOSE");
    }

    step1 = 4;
    setTimer(seq1,5000);
  }
  else if (step1 == 4)
  {
    mode1(1);
    step1 = 5;
    write("CAN1: STANDBY");
    setTimer(seq1,3000);
  }
  else if (step1 == 5)
  {
    mode1(0);
    write("CAN1: OFF");

    cycle1++;

    if (cycle1 < 4)
    {
      step1 = 0;
      setTimer(seq1,2000);
    }
    else
    {
      step1 = 6;
      write("CAN1: TEST COMPLETE");
      checkFinished();
    }
  }
}


void sequence2()
{
  if (step2 == 0)
  {
    mode2(1); step2=1;
    write("CAN2: STANDBY");
    setTimer(seq2,5000);
  }
  else if (step2 == 1)
  {
    mode2(3); step2=2;
    write("CAN2: FLOAT");
    setTimer(seq2,5000);
  }
  else if (step2 == 2)
  {
    if (sys2 != 3) isolation2(0);
    step2=3;
    setTimer(seq2,1000);
  }
  else if (step2 == 3)
  {
    if (sys2 != 3) isolation2(1);
    step2=4;
    setTimer(seq2,5000);
  }
  else if (step2 == 4)
  {
    mode2(1); step2=5;
    write("CAN2: STANDBY");
    setTimer(seq2,3000);
  }
  else if (step2 == 5)
  {
    mode2(0);
    write("CAN2: OFF");
    cycle2++;

    if (cycle2 < 4)
    {
      step2=0;
      setTimer(seq2,2000);
    }
    else
    {
      step2=6;
      write("CAN2: TEST COMPLETE");
      checkFinished();
    }
  }
}


void sequence3()
{
  if (step3 == 0)
  {
    mode3(1); step3=1;
    write("CAN3: STANDBY");
    setTimer(seq3,5000);
  }
  else if (step3 == 1)
  {
    mode3(3); step3=2;
    write("CAN3: FLOAT");
    setTimer(seq3,5000);
  }
  else if (step3 == 2)
  {
    if (sys3 != 3) isolation3(0);
    step3=3;
    setTimer(seq3,1000);
  }
  else if (step3 == 3)
  {
    if (sys3 != 3) isolation3(1);
    step3=4;
    setTimer(seq3,5000);
  }
  else if (step3 == 4)
  {
    mode3(1); step3=5;
    write("CAN3: STANDBY");
    setTimer(seq3,3000);
  }
  else if (step3 == 5)
  {
    mode3(0);
    write("CAN3: OFF");
    cycle3++;

    if (cycle3 < 4)
    {
      step3=0;
      setTimer(seq3,2000);
    }
    else
    {
      step3=6;
      write("CAN3: TEST COMPLETE");
      checkFinished();
    }
  }
}


void sequence4()
{
  if (step4 == 0)
  {
    mode4(1); step4=1;
    write("CAN4: STANDBY");
    setTimer(seq4,5000);
  }
  else if (step4 == 1)
  {
    mode4(3); step4=2;
    write("CAN4: FLOAT");
    setTimer(seq4,5000);
  }
  else if (step4 == 2)
  {
    if (sys4 != 3) isolation4(0);
    step4=3;
    setTimer(seq4,1000);
  }
  else if (step4 == 3)
  {
    if (sys4 != 3) isolation4(1);
    step4=4;
    setTimer(seq4,5000);
  }
  else if (step4 == 4)
  {
    mode4(1); step4=5;
    write("CAN4: STANDBY");
    setTimer(seq4,3000);
  }
  else if (step4 == 5)
  {
    mode4(0);
    write("CAN4: OFF");
    cycle4++;

    if (cycle4 < 4)
    {
      step4=0;
      setTimer(seq4,2000);
    }
    else
    {
      step4=6;
      write("CAN4: TEST COMPLETE");
      checkFinished();
    }
  }
}


void sequence5()
{
  if (step5 == 0)
  {
    mode5(1); step5=1;
    write("CAN5: STANDBY");
    setTimer(seq5,5000);
  }
  else if (step5 == 1)
  {
    mode5(3); step5=2;
    write("CAN5: FLOAT");
    setTimer(seq5,5000);
  }
  else if (step5 == 2)
  {
    if (sys5 != 3) isolation5(0);
    step5=3;
    setTimer(seq5,1000);
  }
  else if (step5 == 3)
  {
    if (sys5 != 3) isolation5(1);
    step5=4;
    setTimer(seq5,5000);
  }
  else if (step5 == 4)
  {
    mode5(1); step5=5;
    write("CAN5: STANDBY");
    setTimer(seq5,3000);
  }
  else if (step5 == 5)
  {
    mode5(0);
    write("CAN5: OFF");
    cycle5++;

    if (cycle5 < 4)
    {
      step5=0;
      setTimer(seq5,2000);
    }
    else
    {
      step5=6;
      write("CAN5: TEST COMPLETE");
      checkFinished();
    }
  }
}


void sequence6()
{
  if (step6 == 0)
  {
    mode6(1); step6=1;
    write("CAN6: STANDBY");
    setTimer(seq6,5000);
  }
  else if (step6 == 1)
  {
    mode6(3); step6=2;
    write("CAN6: FLOAT");
    setTimer(seq6,5000);
  }
  else if (step6 == 2)
  {
    if (sys6 != 3) isolation6(0);
    step6=3;
    setTimer(seq6,1000);
  }
  else if (step6 == 3)
  {
    if (sys6 != 3) isolation6(1);
    step6=4;
    setTimer(seq6,5000);
  }
  else if (step6 == 4)
  {
    mode6(1); step6=5;
    write("CAN6: STANDBY");
    setTimer(seq6,3000);
  }
  else if (step6 == 5)
  {
    mode6(0);
    write("CAN6: OFF");
    cycle6++;

    if (cycle6 < 4)
    {
      step6=0;
      setTimer(seq6,2000);
    }
    else
    {
      step6=6;
      write("CAN6: TEST COMPLETE");
      checkFinished();
    }
  }
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
   ISOLATION
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
   SEND CORRECT CONTROL MESSAGE
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


/* =========================================================
   FINISH

   Stop when every DETECTED channel has completed.
   Undetected channels do NOT block completion.
   ========================================================= */

void checkFinished()
{
  if ((sys1==0 || step1==6) &&
      (sys2==0 || step2==6) &&
      (sys3==0 || step3==6) &&
      (sys4==0 || step4==6) &&
      (sys5==0 || step5==6) &&
      (sys6==0 || step6==6))
  {
    write("ALL ACTIVE CHANNELS COMPLETE");
    write("FINAL OFF - WAITING 2 SEC BEFORE STOP");

    setTimer(stopTimer,2000);
  }
}


on timer stopTimer
{
  write("TEST COMPLETE - STOPPING MEASUREMENT");

  stop();
}