

void updateMonitor()
{
  long remaining;
  long cycleElapsed;

  long rh, rm, rs;
  long th, tm, ts;
  long ch, cm, cs;

  char remainingText[32];
  char totalText[32];
  char cycleText[32];

  remaining = 72002 - elapsedSec;

  if(remaining < 0)
    remaining = 0;

  cycleElapsed = 0;

  if(cycle > 0)
  {
    cycleElapsed = elapsedSec - cycleStartSec;

    if(cycleElapsed < 0)
      cycleElapsed = 0;

    if(cycleElapsed > 18000)
      cycleElapsed = 18000;
  }

  // Convert remaining time
  rh = remaining / 3600;
  rm = (remaining % 3600) / 60;
  rs = remaining % 60;

  // Convert total elapsed time
  th = elapsedSec / 3600;
  tm = (elapsedSec % 3600) / 60;
  ts = elapsedSec % 60;

  // Convert cycle elapsed time
  ch = cycleElapsed / 3600;
  cm = (cycleElapsed % 3600) / 60;
  cs = cycleElapsed % 60;

  snprintf(remainingText, elcount(remainingText),
           "%02d:%02d:%02d", rh, rm, rs);

  snprintf(totalText, elcount(totalText),
           "%02d:%02d:%02d", th, tm, ts);

  snprintf(cycleText, elcount(cycleText),
           "%02d:%02d:%02d", ch, cm, cs);

  // Existing numeric monitors
  @sysvar::TestMonitor::CurrentCycle = cycle;
  @sysvar::TestMonitor::TotalElapsedSec = elapsedSec;
  @sysvar::TestMonitor::RemainingSec = remaining;
  @sysvar::TestMonitor::CycleElapsedSec = cycleElapsed;

  // New formatted time monitors
  sysSetVariableString(
    sysvar::TestMonitor::RemainingTime,
    remainingText);

  sysSetVariableString(
    sysvar::TestMonitor::TotalElapsedTime,
    totalText);

  sysSetVariableString(
    sysvar::TestMonitor::CycleElapsedTime,
    cycleText);
}

