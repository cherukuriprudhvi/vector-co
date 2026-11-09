


/* ============================================================
   TWO CYCLE SHORT TEST

   INITIAL:
     OFF       2 SEC
     STANDBY   2 SEC

   CYCLE 1:
     FLOAT     5 SEC
       WAIT WITH ISOLATION CLOSED  1 SEC
       ISOLATION OPEN             1 SEC
       ISOLATION CLOSE            3 SEC
     STANDBY   2 SEC

   CYCLE 2:
     FLOAT     5 SEC
       WAIT WITH ISOLATION CLOSED  1 SEC
       ISOLATION OPEN             1 SEC
       ISOLATION CLOSE            3 SEC
     STANDBY   2 SEC

   FINAL:
     OFF

   TOTAL: 18 SECONDS

   48V EPAS:
     ISOLATION COMMAND SKIPPED
   ============================================================ */

on timer seqTimer
{
  if(!testRunning)
    return;

  /* INITIAL STANDBY */

  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("STARTUP - STANDBY - 2 SEC");

    step=1;
    setTimer(seqTimer,2000);
  }

  /* CYCLE 1 - FLOAT START */

  else if(step==1)
  {
    @sysvar::TestMonitor::CurrentCycle = 1;
    cycleStartSec = elapsedSec;
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
    write("CYCLE 1 - FLOAT CONTINUES - 3 SEC");

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

  /* CYCLE 2 - FLOAT START */

  else if(step==5)
  {
    @sysvar::TestMonitor::CurrentCycle = 2;
    cycleStartSec = elapsedSec;
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
    write("CYCLE 2 - FLOAT CONTINUES - 3 SEC");

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

  /* TEST COMPLETE */

  else if(step==9)
  {
    setMode(0);
    setIsolation(1);

    /* Transmit final OFF command */
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

    write("==========================================");
    write("2 CYCLE SHORT TEST COMPLETE");
    write("TOTAL DURATION - 18 SECONDS");
    write("FINAL OFF COMMAND TRANSMITTED");
    write("MEASUREMENT REMAINS RUNNING");
    write("==========================================");
  }
}
