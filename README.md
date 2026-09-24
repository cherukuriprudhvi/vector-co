

variables
{
  msTimer logTimer;
  int logState = 0;
}

on start
{
  // Start first logging segment
  trigger();
  logState = 1;
  write("LOGGING ON - Segment 1");

  setTimer(logTimer, 30000);
}

on timer logTimer
{
  if (logState == 1)
  {
    // Toggle OFF -> closes current segment
    trigger();
    logState = 0;
    write("LOGGING OFF");

    // short gap before starting next file
    setTimer(logTimer, 100);
  }
  else
  {
    // Toggle ON -> starts new segment
    trigger();
    logState = 1;
    write("LOGGING ON - New segment");

    setTimer(logTimer, 30000);
  }
}