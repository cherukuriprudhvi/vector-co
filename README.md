


/*
  FIVE-DAY CANALYZER CAPL CONTROLLER

  Startup:
    OFF       2 seconds
    STANDBY   1 second

  Repeat 5 times:
    FLOAT + isolation OPEN
    1 second later: isolation CLOSE
    FLOAT for 18 hours total
    STANDBY for 6 hours

  End after cycle 5.

  Mode values:
    0 = OFF
    1 = STANDBY
    3 = FLOAT

  Isolation:
    0 = OPEN
    1 = CLOSE

  IMPORTANT:
  Connect the three functions below to your
  verified DBC messages before running hardware.
*/

variables
{
  msTimer sequenceTimer;
  msTimer transmitTimer;

  int phase = 0;
  int cycle = 0;
  int running = 0;

  int requestedMode = 0;
  int requestedIsolation = 1;

  long FLOAT_MS = 64800000;
  long STANDBY_MS = 21600000;
}

/*
  Replace these function bodies with the
  verified message/signal assignments
  for your CAN channels.
*/

void setMode(int mode)
{
  requestedMode = mode;

  // TODO: Assign requested mode to the
  // correct DBC signal for each active system.
}

void setIsolation(int value)
{
  requestedIsolation = value;

  // TODO: Assign isolation command for
  // EBB, EMB, and 12V EPAS.
  // Skip isolation for 48V EPAS.
}

void sendAllMessages()
{
  // TODO: Transmit all required CAN FD
  // network management, BodyInfo,
  // control and information messages.
  //
  // Preserve the verified 100 ms,
  // 500 ms and 1000 ms periods.
}

on start
{
  running = 1;
  cycle = 0;
  phase = 0;

  setIsolation(1);
  setMode(0);

  write("5-DAY TEST STARTED");
  write("OFF - 2 SECONDS");

  setTimer(transmitTimer, 100);
  setTimer(sequenceTimer, 2000);
}

on timer transmitTimer
{
  if (running)
  {
    sendAllMessages();
    setTimer(transmitTimer, 100);
  }
}

on timer sequenceTimer
{
  if (!running)
  {
    return;
  }

  switch (phase)
  {
    case 0:
      setMode(1);

      write("STANDBY - 1 SECOND");

      phase = 1;
      setTimer(sequenceTimer, 1000);
      break;

    case 1:
      cycle++;

      setMode(3);
      setIsolation(0);

      write("CYCLE %d: FLOAT, ISOLATION OPEN",
            cycle);

      phase = 2;
      setTimer(sequenceTimer, 1000);
      break;

    case 2:
      setIsolation(1);

      write("CYCLE %d: ISOLATION CLOSED",
            cycle);
      write("FLOAT CONTINUES");

      phase = 3;

      // Remaining 18 hours after
      // the 1-second OPEN interval.
      setTimer(sequenceTimer, 64799000);
      break;

    case 3:
      setMode(1);

      write("CYCLE %d: FLOAT COMPLETE",
            cycle);
      write("STANDBY - 6 HOURS");

      phase = 4;
      setTimer(sequenceTimer, 21600000);
      break;

    case 4:
      if (cycle >= 5)
      {
        write("ALL 5 CYCLES COMPLETE");
        write("5-DAY TEST FINISHED");

        running = 0;

        cancelTimer(transmitTimer);
        cancelTimer(sequenceTimer);

        stop();
      }
      else
      {
        setMode(3);
        setIsolation(0);

        cycle++;

        write("CYCLE %d: FLOAT, ISOLATION OPEN",
              cycle);

        phase = 2;
        setTimer(sequenceTimer, 1000);
      }
      break;
  }
}

on stopMeasurement
{
  running = 0;

  cancelTimer(sequenceTimer);
  cancelTimer(transmitTimer);

  write("MEASUREMENT STOPPED");
}
