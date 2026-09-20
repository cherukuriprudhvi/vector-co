

variables
{
  msTimer stepTimer;
  msTimer txTimer;

  int step = 0;

  message EnergyMgmtBodyCtrl_4 ctrlMsg;
}

on start
{
  // OFF
  ctrlMsg.EMduleMde_D_Rq3 = 0;
  ctrlMsg.IsolSwtch_B_Cmd3 = 1;   // Close

  output(ctrlMsg);

  setTimer(txTimer, 100);     // cyclic send every 100 ms
  setTimer(stepTimer, 5000);  // wait 5 sec
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
    // STANDBY
    ctrlMsg.EMduleMde_D_Rq3 = 1;
    step = 1;
    setTimer(stepTimer, 5000);
  }

  else if (step == 1)
  {
    // FLOAT
    ctrlMsg.EMduleMde_D_Rq3 = 3;
    step = 2;
    setTimer(stepTimer, 4000);
  }

  else if (step == 2)
  {
    // Isolation OPEN
    ctrlMsg.IsolSwtch_B_Cmd3 = 0;
    step = 3;
    setTimer(stepTimer, 2000);
  }

  else if (step == 3)
  {
    // Isolation CLOSE
    ctrlMsg.IsolSwtch_B_Cmd3 = 1;
    step = 4;

    write("CAN1 EPAS startup sequence complete");
  }
}