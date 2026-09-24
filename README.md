

variables
{
  msTimer stepTimer;
  msTimer txTimer;

  int system = 0;
  int step = 0;

  // CAN1 / DBC1
  message DBC1::EnergyMgmtBodyCtrl_1 ebb;
  message DBC1::EnergyMgmtBodyCtrl_2 emb;
  message DBC1::EnergyMgmtBodyCtrl_3 v48;
  message DBC1::EnergyMgmtBodyCtrl_4 epas;
}


/* =========================================
   AUTO-DETECT SYSTEM ON CAN1
   ========================================= */

on message CAN1.*
{
  if (system != 0)
    return;

  // EBB
  if (this.id == 273 ||
      this.id == 304 ||
      this.id == 544 ||
      this.id == 560 ||
      this.id == 1024)
  {
    system = 1;
    write("CAN1 DETECTED: EBB");
    startControl();
  }

  // EMB
  else if (this.id == 272 ||
           this.id == 305 ||
           this.id == 545 ||
           this.id == 561 ||
           this.id == 769 ||
           this.id == 1025)
  {
    system = 2;
    write("CAN1 DETECTED: EMB");
    startControl();
  }

  // 48V EPAS
  else if (this.id == 256 ||
           this.id == 306 ||
           this.id == 770)
  {
    system = 3;
    write("CAN1 DETECTED: 48V EPAS");
    startControl();
  }

  // EPAS
  else if (this.id == 309 ||
           this.id == 1026)
  {
    system = 4;
    write("CAN1 DETECTED: EPAS");
    startControl();
  }
}


/* =========================================
   START SEQUENCE
   ========================================= */

void startControl()
{
  step = 0;

  // Start in OFF
  setMode(0);

  // Keep transmitting control message every 100 ms
  setTimer(txTimer, 100);

  // OFF for 5 seconds
  setTimer(stepTimer, 5000);

  write("CAN1: OFF");
}


/* =========================================
   CYCLIC TRANSMISSION - 100 ms
   ========================================= */

on timer txTimer
{
  sendMsg();
  setTimer(txTimer, 100);
}


/* =========================================
   COMPLETE MODE SEQUENCE
   ========================================= */

on timer stepTimer
{
  if (step == 0)
  {
    // OFF -> STANDBY
    setMode(1);

    step = 1;

    write("CAN1: STANDBY");

    setTimer(stepTimer, 5000);
  }

  else if (step == 1)
  {
    // STANDBY -> FLOAT
    setMode(3);

    step = 2;

    write("CAN1: FLOAT");

    // 48V EPAS has no isolation
    if (system == 3)
    {
      step = 4;
      setTimer(stepTimer, 5000);
    }
    else
    {
      // Wait 4 sec before isolation
      setTimer(stepTimer, 4000);
    }
  }

  else if (step == 2)
  {
    // Isolation OPEN
    setIsolation(0);

    step = 3;

    write("CAN1: ISOLATION OPEN");

    setTimer(stepTimer, 2000);
  }

  else if (step == 3)
  {
    // Isolation CLOSE
    setIsolation(1);

    step = 4;

    write("CAN1: ISOLATION CLOSE");

    // Stay FLOAT for test
    setTimer(stepTimer, 5000);
  }

  else if (step == 4)
  {
    // FLOAT -> STANDBY
    setMode(1);

    step = 5;

    write("CAN1: STANDBY");

    setTimer(stepTimer, 5000);
  }

  else if (step == 5)
  {
    // STANDBY -> OFF
    setMode(0);

    step = 6;

    write("CAN1: OFF");
    write("CAN1: SEQUENCE COMPLETE");
  }
}


/* =========================================
   SET MODE
   ========================================= */

void setMode(int value)
{
  // EBB
  if (system == 1)
    ebb.EMduleMde_D_Rq = value;

  // EMB
  else if (system == 2)
    emb.EMduleMde_D_Rq2 = value;

  // 48V EPAS
  else if (system == 3)
    v48.UCapMduleMde_D_Rq = value;

  // EPAS
  else if (system == 4)
    epas.EMduleMde_D_Rq3 = value;

  sendMsg();
}


/* =========================================
   SET ISOLATION
   ========================================= */

void setIsolation(int value)
{
  // EBB
  if (system == 1)
    ebb.IsolSwtch_B_Cmd = value;

  // EMB
  else if (system == 2)
    emb.IsolSwtch_B_Cmd2 = value;

  // EPAS
  else if (system == 4)
    epas.IsolSwtch_B_Cmd3 = value;

  sendMsg();
}


/* =========================================
   SEND ONLY CORRECT CONTROL MESSAGE
   ========================================= */

void sendMsg()
{
  if (system == 1)
    output(ebb);       // EBB 528 / 0x210

  else if (system == 2)
    output(emb);       // EMB 529 / 0x211

  else if (system == 3)
    output(v48);       // 48V EPAS 530 / 0x212

  else if (system == 4)
    output(epas);      // EPAS 531 / 0x213
}