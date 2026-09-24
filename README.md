

variables
{
  msTimer stepTimer;
  msTimer txTimer;

  int system = 0;
  int step = 0;

  message DBC1::EnergyMgmtBodyCtrl_1 ebbMsg;
  message DBC1::EnergyMgmtBodyCtrl_2 embMsg;
  message DBC1::EnergyMgmtBodyCtrl_3 v48Msg;
  message DBC1::EnergyMgmtBodyCtrl_4 epasMsg;
}


/* ==================================================
   CAN1 AUTO DETECTION
   ================================================== */

on message CAN1.*
{
  if (system != 0)
    return;

  /* EBB */
  if (this.id == 273 ||
      this.id == 304 ||
      this.id == 544 ||
      this.id == 560 ||
      this.id == 1024)
  {
    system = 1;
    write("CAN1 DETECTED: EBB");
    startSequence();
  }

  /* EMB */
  else if (this.id == 272 ||
           this.id == 305 ||
           this.id == 545 ||
           this.id == 561 ||
           this.id == 769 ||
           this.id == 1025)
  {
    system = 2;
    write("CAN1 DETECTED: EMB");
    startSequence();
  }

  /* 48V EPAS */
  else if (this.id == 256 ||
           this.id == 306 ||
           this.id == 770)
  {
    system = 3;
    write("CAN1 DETECTED: 48V EPAS");
    startSequence();
  }

  /* EPAS */
  else if (this.id == 309 ||
           this.id == 1026)
  {
    system = 4;
    write("CAN1 DETECTED: EPAS");
    startSequence();
  }
}


/* ==================================================
   START
   ================================================== */

void startSequence()
{
  step = 0;

  /* OFF */
  changeMode(0);

  /* Isolation starts CLOSED */
  if (system != 3)
    changeIsolation(1);

  /*
     Same pattern as your original working EBB:
     transmit selected control message every 100 ms
  */
  sendSelectedMessage();

  setTimer(txTimer, 100);
  setTimer(stepTimer, 5000);

  write("CAN1: OFF");
}


/* ==================================================
   PERIODIC CONTROL MESSAGE
   ================================================== */

on timer txTimer
{
  sendSelectedMessage();

  setTimer(txTimer, 100);
}


/* ==================================================
   MODE SEQUENCE
   ================================================== */

on timer stepTimer
{
  /* OFF -> STANDBY */
  if (step == 0)
  {
    changeMode(1);

    step = 1;

    write("CAN1: STANDBY");

    setTimer(stepTimer, 5000);
  }


  /* STANDBY -> FLOAT */
  else if (step == 1)
  {
    changeMode(3);

    step = 2;

    write("CAN1: FLOAT");


    /* 48V EPAS - NO isolation */
    if (system == 3)
    {
      step = 4;
      setTimer(stepTimer, 5000);
    }
    else
    {
      /* FLOAT first, then isolation */
      setTimer(stepTimer, 4000);
    }
  }


  /* ISOLATION OPEN */
  else if (step == 2)
  {
    changeIsolation(0);

    step = 3;

    write("CAN1: ISOLATION OPEN");

    setTimer(stepTimer, 2000);
  }


  /* ISOLATION CLOSE */
  else if (step == 3)
  {
    changeIsolation(1);

    step = 4;

    write("CAN1: ISOLATION CLOSE");

    setTimer(stepTimer, 5000);
  }


  /* FLOAT -> STANDBY */
  else if (step == 4)
  {
    changeMode(1);

    step = 5;

    write("CAN1: STANDBY");

    setTimer(stepTimer, 5000);
  }


  /* STANDBY -> OFF */
  else if (step == 5)
  {
    changeMode(0);

    step = 6;

    write("CAN1: OFF");
    write("CAN1: SEQUENCE COMPLETE");
  }
}


/* ==================================================
   CHANGE MODE
   IMPORTANT:
   NO output() here.
   Only change the value.
   ================================================== */

void changeMode(int value)
{
  if (system == 1)
  {
    ebbMsg.EMduleMde_D_Rq = value;
  }

  else if (system == 2)
  {
    embMsg.EMduleMde_D_Rq2 = value;
  }

  else if (system == 3)
  {
    v48Msg.UCapMduleMde_D_Rq = value;
  }

  else if (system == 4)
  {
    epasMsg.EMduleMde_D_Rq3 = value;
  }
}


/* ==================================================
   CHANGE ISOLATION
   IMPORTANT:
   NO output() here.
   ================================================== */

void changeIsolation(int value)
{
  if (system == 1)
  {
    ebbMsg.IsolSwtch_B_Cmd = value;
  }

  else if (system == 2)
  {
    embMsg.IsolSwtch_B_Cmd2 = value;
  }

  else if (system == 4)
  {
    epasMsg.IsolSwtch_B_Cmd3 = value;
  }
}


/* ==================================================
   ONLY PLACE THAT TRANSMITS CONTROL MESSAGE
   ================================================== */

void sendSelectedMessage()
{
  if (system == 1)
  {
    output(ebbMsg);       // 528 / 0x210
  }

  else if (system == 2)
  {
    output(embMsg);       // 529 / 0x211
  }

  else if (system == 3)
  {
    output(v48Msg);       // 530 / 0x212
  }

  else if (system == 4)
  {
    output(epasMsg);      // 531 / 0x213
  }
}