
variables
{
  msTimer stepTimer;
  msTimer txTimer;

  int step = 0;

  // EBB control message = ID 0x210 / decimal 528
  message DBC1::EnergyMgmtBodyCtrl_1 ctrlMsg;
}

on start
{
  // Start with OFF + Isolation CLOSE
  ctrlMsg.EMduleMde_D_Rq = 0;
  ctrlMsg.IsolSwtch_B_Cmd = 1;

  output(ctrlMsg);

  // Send control message continuously every 100 ms
  setTimer(txTimer, 100);

  // Stay OFF for 5 seconds
  setTimer(stepTimer, 5000);

  write("EBB CAN1: OFF");
}

on timer txTimer
{
  output(ctrlMsg);

  // Continue transmitting every 100 ms
  setTimer(txTimer, 100);
}

on timer stepTimer
{
  if (step == 0)
  {
    // OFF -> STANDBY
    ctrlMsg.EMduleMde_D_Rq = 1;

    step = 1;
    setTimer(stepTimer, 5000);

    write("EBB CAN1: STANDBY");
  }
  else if (step == 1)
  {
    // STANDBY -> FLOAT
    ctrlMsg.EMduleMde_D_Rq = 3;

    step = 2;
    setTimer(stepTimer, 4000);

    write("EBB CAN1: FLOAT");
  }
  else if (step == 2)
  {
    // Isolation OPEN
    ctrlMsg.IsolSwtch_B_Cmd = 0;

    step = 3;
    setTimer(stepTimer, 2000);

    write("EBB CAN1: Isolation OPEN");
  }
  else if (step == 3)
  {
    // Isolation CLOSE
    ctrlMsg.IsolSwtch_B_Cmd = 1;

    step = 4;

    write("EBB CAN1: Startup sequence complete");
  }
}
