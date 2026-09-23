

variables
{
  msTimer stepTimer;
  msTimer txTimer;
  int step = 0;

  message DBC1::EnergyMgmtBodyCtrl_1 ctrlMsg;
}

on start
{
  // OFF + Isolation CLOSED
  ctrlMsg.EMduleMde_D_Rq = 0;
  ctrlMsg.IsolSwtch_B_Cmd = 1;

  output(ctrlMsg);
  setTimer(txTimer, 100);
  setTimer(stepTimer, 1000);

  write("EBB: OFF");
}

on timer txTimer
{
  output(ctrlMsg);
  setTimer(txTimer, 100);
}

on timer stepTimer
{
  if (step == 0)
  {
    // STANDBY for 1 sec
    ctrlMsg.EMduleMde_D_Rq = 1;
    step = 1;
    setTimer(stepTimer, 1000);
    write("EBB: STANDBY");
  }
  else if (step == 1)
  {
    // FLOAT
    ctrlMsg.EMduleMde_D_Rq = 3;
    step = 2;
    setTimer(stepTimer, 1000);
    write("EBB: FLOAT");
  }
  else if (step == 2)
  {
    // After 1 sec in FLOAT -> Isolation OPEN
    ctrlMsg.IsolSwtch_B_Cmd = 0;
    step = 3;
    setTimer(stepTimer, 1000);
    write("EBB: ISOLATION OPEN");
  }
  else if (step == 3)
  {
    // Isolation CLOSE
    ctrlMsg.IsolSwtch_B_Cmd = 1;
    step = 4;
    setTimer(stepTimer, 2000);
    write("EBB: ISOLATION CLOSE - FLOAT");
  }
  else if (step == 4)
  {
    // STANDBY for 1 sec
    ctrlMsg.EMduleMde_D_Rq = 1;
    step = 5;
    setTimer(stepTimer, 1000);
    write("EBB: STANDBY");
  }
  else if (step == 5)
  {
    // Final OFF
    ctrlMsg.EMduleMde_D_Rq = 0;
    ctrlMsg.IsolSwtch_B_Cmd = 1;
    step = 6;

    write("EBB: OFF - COMPLETE");
  }
}