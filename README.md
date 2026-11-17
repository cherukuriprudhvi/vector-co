


on timer seqTimer
{
  if(!testRunning)
    return;

  /* MANUAL STOP */
  if(step==10)
  {
    setMode(0);
    setIsolation(1);
    send100();

    write("MANUAL STOP - OFF");

    testRunning=0;
    finalStopPending=1;
    step=0;

    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(monitorTimer);

    setTimer(stopTimer,500);
    return;
  }

  /* INITIAL OFF -> STANDBY */
  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("INITIAL STANDBY - 1 SECOND");

    step=1;
    setTimer(seqTimer,1000);
  }

  /* INITIAL STANDBY -> FLOAT CYCLE 1 */
  else if(step==1)
  {
    cycle=1;
    cycleStartSec=elapsedSec;

    setMode(3);
    setIsolation(1);

    write("CYCLE 1 FLOAT START");

    step=2;
    setTimer(seqTimer,1000);
  }

  /* FLOAT - ISOLATION OPEN */
  else if(step==2)
  {
    setIsolation(0);

    write("CYCLE %d - ISOLATION OPEN",cycle);

    step=3;
    setTimer(seqTimer,1000);
  }

  /* FLOAT - ISOLATION CLOSED */
  else if(step==3)
  {
    setIsolation(1);

    write("CYCLE %d - ISOLATION CLOSED",cycle);

    step=4;
    setTimer(seqTimer,3000);
  }

  /* FLOAT COMPLETE -> STANDBY */
  else if(step==4)
  {
    setMode(1);
    setIsolation(1);

    write("CYCLE %d FLOAT COMPLETE",cycle);
    write("STANDBY - 1 SECOND");

    step=5;
    setTimer(seqTimer,1000);
  }

  /* NEXT CYCLE OR FINAL OFF */
  else if(step==5)
  {
    if(cycle<2)
    {
      cycle++;
      cycleStartSec=elapsedSec;

      setMode(3);
      setIsolation(1);

      write("CYCLE %d FLOAT START",cycle);

      step=2;
      setTimer(seqTimer,1000);
    }
    else
    {
      setMode(0);
      setIsolation(1);
      send100();

      write("TWO CYCLES COMPLETE");
      write("FINAL OFF - 500 MS");

      elapsedSec=14;
      updateMonitor();

      testRunning=0;
      finalStopPending=1;
      step=0;

      cancelTimer(t500);
      cancelTimer(t1000);
      cancelTimer(monitorTimer);

      setTimer(stopTimer,500);
    }
  }
}
