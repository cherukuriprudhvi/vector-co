
void updateMonitor()
{
  int i;
  int waiting;
  int active;

  long remaining;
  long channelRemaining;
  long cycleElapsed;

  char remainingText[32];
  char totalText[32];
  char cycleText[32];

  remaining=0;
  waiting=0;
  active=0;
  cycleElapsed=0;

  for(i=0;i<6;i++)
  {
    if(sys[i]==0)
      continue;

    active++;

    if(state[i]==1 || state[i]==2)
      waiting=1;

    channelRemaining=
      (floatDuration-floatTicks[i]+9)/10;

    if(channelRemaining<0)
      channelRemaining=0;

    if(channelRemaining>remaining)
      remaining=channelRemaining;

    if(floatTicks[i]/10>cycleElapsed)
      cycleElapsed=floatTicks[i]/10;
  }

  if(active==0)
  {
    remaining=300;
    cycleElapsed=0;
  }

  if(cycleElapsed>300)
    cycleElapsed=300;

  if(remaining>300)
    remaining=300;

  if(remaining<0)
    remaining=0;

  snprintf(remainingText,
           elcount(remainingText),
           "%02d:%02d:%02d",
           remaining/3600,
           (remaining%3600)/60,
           remaining%60);

  snprintf(totalText,
           elcount(totalText),
           "%02d:%02d:%02d",
           elapsedSec/3600,
           (elapsedSec%3600)/60,
           elapsedSec%60);

  snprintf(cycleText,
           elcount(cycleText),
           "%02d:%02d:%02d",
           cycleElapsed/3600,
           (cycleElapsed%3600)/60,
           cycleElapsed%60);

  @sysvar::TestMonitor::CurrentCycle=cycle;

  @sysvar::TestMonitor::TotalElapsedSec=
    elapsedSec;

  @sysvar::TestMonitor::RemainingSec=
    remaining;

  @sysvar::TestMonitor::CycleElapsedSec=
    cycleElapsed;

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