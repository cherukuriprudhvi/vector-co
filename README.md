


on timer seqTimer
{
  if(!testRunning)
    return;

  /* INITIAL OFF -> STANDBY */

  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("INITIAL STANDBY - 2 SEC");

    step=1;
    setTimer(seqTimer,2000);
  }

  /* CYCLE 1 - FLOAT START, ISOLATION CLOSED */

  else if(step==1)
  {
    @sysvar::TestMonitor::CurrentCycle=1;
    cycleStartSec=elapsedSec;
    updateMonitor();

    setMode(3);
    setIsolation(1);

    write("CYCLE 1 - FLOAT START - WAIT 1 SEC");

    step=2;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 1 - ISOLATION OPEN */

  else if(step==2)
  {
    setIsolation(0);

    write("CYCLE 1 - ISOLATION OPEN - 1 SEC");

    step=3;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 1 - ISOLATION CLOSE */

  else if(step==3)
  {
    setIsolation(1);

    write("CYCLE 1 - ISOLATION CLOSE");
    write("FLOAT CONTINUES - 3 SEC");

    step=4;
    setTimer(seqTimer,3000);
  }

  /* CYCLE 1 - STANDBY */

  else if(step==4)
  {
    setMode(1);
    setIsolation(1);

    write("CYCLE 1 - STANDBY - 2 SEC");

    step=5;
    setTimer(seqTimer,2000);
  }

  /* CYCLE 2 - FLOAT START, ISOLATION CLOSED */

  else if(step==5)
  {
    @sysvar::TestMonitor::CurrentCycle=2;
    cycleStartSec=elapsedSec;
    updateMonitor();

    setMode(3);
    setIsolation(1);

    write("CYCLE 2 - FLOAT START - WAIT 1 SEC");

    step=6;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 2 - ISOLATION OPEN */

  else if(step==6)
  {
    setIsolation(0);

    write("CYCLE 2 - ISOLATION OPEN - 1 SEC");

    step=7;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 2 - ISOLATION CLOSE */

  else if(step==7)
  {
    setIsolation(1);

    write("CYCLE 2 - ISOLATION CLOSE");
    write("FLOAT CONTINUES - 3 SEC");

    step=8;
    setTimer(seqTimer,3000);
  }

  /* CYCLE 2 - STANDBY */

  else if(step==8)
  {
    setMode(1);
    setIsolation(1);

    write("CYCLE 2 - STANDBY - 2 SEC");

    step=9;
    setTimer(seqTimer,2000);
  }

  /* FINAL OFF */

  else if(step==9)
  {
    setMode(0);
    setIsolation(1);

    send100();

    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);
    cancelTimer(monitorTimer);

    testRunning=0;
    step=0;

    elapsedSec=18;
    updateMonitor();

    write("==================================");
    write("2 CYCLES COMPLETED");
    write("TOTAL TIME = 18 SECONDS");
    write("FINAL OFF COMMAND SENT");
    write("==================================");
  }
}
