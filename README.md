


void updateMonitor()
{
  long remaining;
  long cycleElapsed;
  long rh,rm,rs;
  long th,tm,ts;
  long ch,cm,cs;

  char remainingText[32];
  char totalText[32];
  char cycleText[32];

  /* TWO CYCLES - TOTAL 14 SECONDS */
  remaining=14-elapsedSec;

  if(remaining<0)
    remaining=0;

  cycleElapsed=0;

  if(cycle>0)
  {
    cycleElapsed=elapsedSec-cycleStartSec;

    if(cycleElapsed<0)
      cycleElapsed=0;

    if(cycleElapsed>6)
      cycleElapsed=6;
  }

  rh=remaining/3600;
  rm=(remaining%3600)/60;
  rs=remaining%60;

  th=elapsedSec/3600;
  tm=(elapsedSec%3600)/60;
  ts=elapsedSec%60;

  ch=cycleElapsed/3600;
  cm=(cycleElapsed%3600)/60;
  cs=cycleElapsed%60;

  snprintf(remainingText,elcount(remainingText),
           "%02d:%02d:%02d",rh,rm,rs);

  snprintf(totalText,elcount(totalText),
           "%02d:%02d:%02d",th,tm,ts);

  snprintf(cycleText,elcount(cycleText),
           "%02d:%02d:%02d",ch,cm,cs);

  @sysvar::TestMonitor::CurrentCycle=cycle;
  @sysvar::TestMonitor::TotalElapsedSec=elapsedSec;
  @sysvar::TestMonitor::RemainingSec=remaining;
  @sysvar::TestMonitor::CycleElapsedSec=cycleElapsed;

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
