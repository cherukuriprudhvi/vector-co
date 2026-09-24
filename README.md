

variables
{
  msTimer modeTimer;
  msTimer txTimer;
  msTimer stopTimer;

  int step = 0;
  int finished = 0;

  message DBC1::EnergyMgmtBodyCtrl_4 ctrlMsg;
}

on start
{
  // Start OFF
  ctrlMsg.EMduleMde_D_Rq3 = 0;
  ctrlMsg.IsolSwtch_B_Cmd3 = 1;

  output(ctrlMsg);

  write("TEST START - OFF");

  setTimer(txTimer, 100);
  setTimer(modeTimer, 10000);
  setTimer(stopTimer, 180000);
}

on timer txTimer
{
  output(ctrlMsg);

  if (!finished)
  {
    setTimer(txTimer, 100);
  }
}

on timer modeTimer
{
  if (finished)
    return;

  step++;

  if ((step % 3) == 1)
  {
    // STANDBY
    ctrlMsg.EMduleMde_D_Rq3 = 1;
    write("MODE -> STANDBY");
  }
  else if ((step % 3) == 2)
  {
    // FLOAT
    ctrlMsg.EMduleMde_D_Rq3 = 3;
    write("MODE -> FLOAT");
  }
  else
  {
    // OFF
    ctrlMsg.EMduleMde_D_Rq3 = 0;
    write("MODE -> OFF");
  }

  setTimer(modeTimer, 10000);
}

on timer stopTimer
{
  finished = 1;

  cancelTimer(modeTimer);

  // Final OFF
  ctrlMsg.EMduleMde_D_Rq3 = 0;
  ctrlMsg.IsolSwtch_B_Cmd3 = 1;

  output(ctrlMsg);

  write("3 MIN TEST COMPLETE - FINAL OFF");
}
