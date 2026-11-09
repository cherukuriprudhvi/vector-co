

/* =====================================================
   TEST MONITOR
   Add these 2 declarations INSIDE existing variables {}
   =====================================================

   int elapsedSec = 0;
   int cycleStartSec = 0;

   Do not add them again if already declared.
*/


void updateMonitor()
{
  int remaining;
  int cycleElapsed;

  remaining = 18 - elapsedSec;
  if(remaining < 0) remaining = 0;

  cycleElapsed = 0;

  if(@sysvar::TestMonitor::CurrentCycle > 0)
  {
    cycleElapsed = elapsedSec - cycleStartSec;
    if(cycleElapsed < 0) cycleElapsed = 0;
    if(cycleElapsed > 7) cycleElapsed = 7;
  }

  @sysvar::TestMonitor::TotalElapsedSec = elapsedSec;
  @sysvar::TestMonitor::RemainingSec = remaining;
  @sysvar::TestMonitor::CycleElapsedSec = cycleElapsed;
}


/* MEASUREMENT START */

on start
{
  sys1 = 0;
  sys2 = 0;

  testRunning = 0;
  step = 0;
  elapsedSec = 0;
  cycleStartSec = 0;

  @sysvar::MasterCtrl::StartTest = 0;
  @sysvar::MasterCtrl::StopTest = 0;
  @sysvar::TestMonitor::CurrentCycle = 0;

  updateMonitor();

  write("MEASUREMENT STARTED - WAITING FOR PANEL");
}


/* PANEL START TEST */

on sysvar MasterCtrl::StartTest
{
  if(@this == 1 && testRunning == 0)
  {
    sys1 = @sysvar::CH1::Module;
    sys2 = @sysvar::CH2::Module;

    if(sys1 == 0 && sys2 == 0)
    {
      write("NO SYSTEM SELECTED");
      @sysvar::MasterCtrl::StartTest = 0;
      return;
    }

    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);

    testRunning = 1;
    step = 0;
    elapsedSec = 0;
    cycleStartSec = 0;

    @sysvar::TestMonitor::CurrentCycle = 0;
    updateMonitor();

    initMessages();

    setMode(0);
    setIsolation(1);

    send100();
    send500();
    send1000();

    setTimer(t100,100);
    setTimer(t500,500);
    setTimer(t1000,1000);

    write("TEST STARTED - INITIAL OFF 2 SEC");

    setTimer(seqTimer,2000);

    @sysvar::MasterCtrl::StartTest = 0;
  }
}


/* PANEL STOP TEST */

on sysvar MasterCtrl::StopTest
{
  if(@this == 1)
  {
    if(testRunning)
    {
      setMode(0);
      setIsolation(1);
      send100();
    }

    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);

    testRunning = 0;
    step = 0;

    write("TEST STOPPED - OFF COMMAND SENT");

    @sysvar::MasterCtrl::StopTest = 0;
  }
}


/* PERIODIC TRANSMISSION */

on timer t100
{
  if(testRunning)
  {
    send100();
    setTimer(t100,100);
  }
}

on timer t500
{
  if(testRunning)
  {
    send500();
    setTimer(t500,500);
  }
}

on timer t1000
{
  if(testRunning)
  {
    elapsedSec++;

    if(elapsedSec > 18)
      elapsedSec = 18;

    updateMonitor();

    send1000();
    setTimer(t1000,1000);
  }
}


/* =====================================================
   TWO CYCLE TEST - TOTAL 18 SECONDS

   INITIAL OFF      2 SEC
   INITIAL STANDBY  2 SEC

   CYCLE 1:
     FLOAT CLOSED   1 SEC
     FLOAT OPEN     1 SEC
     FLOAT CLOSED   3 SEC
     STANDBY        2 SEC

   CYCLE 2:
     FLOAT CLOSED   1 SEC
     FLOAT OPEN     1 SEC
     FLOAT CLOSED   3 SEC
     STANDBY        2 SEC

   FINAL OFF
   ===================================================== */

on timer seqTimer
{
  if(!testRunning) return;

  /* INITIAL STANDBY */

  if(step == 0)
  {
    setMode(1);
    setIsolation(1);

    write("INITIAL STANDBY - 2 SEC");

    step = 1;
    setTimer(seqTimer,2000);
  }

  /* CYCLE 1 - FLOAT START */

  else if(step == 1)
  {
    @sysvar::TestMonitor::CurrentCycle = 1;
    cycleStartSec = elapsedSec;
    updateMonitor();

    setMode(3);
    setIsolation(1);

    write("CYCLE 1 FLOAT - WAIT 1 SEC");

    step = 2;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 1 - OPEN ISOLATION */

  else if(step == 2)
  {
    setIsolation(0);

    write("CYCLE 1 ISOLATION OPEN - 1 SEC");

    step = 3;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 1 - CLOSE ISOLATION */

  else if(step == 3)
  {
    setIsolation(1);

    write("CYCLE 1 ISOLATION CLOSE - FLOAT 3 SEC");

    step = 4;
    setTimer(seqTimer,3000);
  }

  /* CYCLE 1 - STANDBY */

  else if(step == 4)
  {
    setMode(1);
    setIsolation(1);

    write("CYCLE 1 STANDBY - 2 SEC");

    step = 5;
    setTimer(seqTimer,2000);
  }

  /* CYCLE 2 - FLOAT START */

  else if(step == 5)
  {
    @sysvar::TestMonitor::CurrentCycle = 2;
    cycleStartSec = elapsedSec;
    updateMonitor();

    setMode(3);
    setIsolation(1);

    write("CYCLE 2 FLOAT - WAIT 1 SEC");

    step = 6;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 2 - OPEN ISOLATION */

  else if(step == 6)
  {
    setIsolation(0);

    write("CYCLE 2 ISOLATION OPEN - 1 SEC");

    step = 7;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 2 - CLOSE ISOLATION */

  else if(step == 7)
  {
    setIsolation(1);

    write("CYCLE 2 ISOLATION CLOSE - FLOAT 3 SEC");

    step = 8;
    setTimer(seqTimer,3000);
  }

  /* CYCLE 2 - STANDBY */

  else if(step == 8)
  {
    setMode(1);
    setIsolation(1);

    write("CYCLE 2 STANDBY - 2 SEC");

    step = 9;
    setTimer(seqTimer,2000);
  }

  /* TEST COMPLETE */

  else if(step == 9)
  {
    setMode(0);
    setIsolation(1);

    send100();

    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);

    testRunning = 0;
    step = 0;

    elapsedSec = 18;
    updateMonitor();

    write("==================================");
    write("2 CYCLES COMPLETED");
    write("TOTAL TIME = 18 SECONDS");
    write("FINAL OFF COMMAND SENT");
    write("==================================");
  }
}