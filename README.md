

variables
{
  msTimer logTimer;
  int logState = 0;
}

on start
{
  // Toggle logging ON immediately
  trigger();
  logState = 1;

  write("LOGGING ON - Segment 1");
  setTimer(logTimer, 30000);
}

on timer logTimer
{
  if (logState == 1)
  {
    // Toggle OFF after 30 sec
    trigger();
    logState = 0;

    write("LOGGING OFF");
    setTimer(logTimer, 100);
  }
  else
  {
    // Toggle ON again = next segment
    trigger();
    logState = 1;

    write("LOGGING ON - New segment");
    setTimer(logTimer, 30000);
  }
}