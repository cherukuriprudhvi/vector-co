on sysvar MasterCtrl::StartTest
{
  if(@this == 1 && testRunning == 0 && finalStopPending == 0)
  {
    sys1=@sysvar::CH1::Module;
    sys2=@sysvar::CH2::Module;
    sys3=@sysvar::CH3::Module;
    sys4=@sysvar::CH4::Module;
    sys5=@sysvar::CH5::Module;
    sys6=@sysvar::CH6::Module;

    if(sys1==0 && sys2==0 && sys3==0 &&
       sys4==0 && sys5==0 && sys6==0)
    {
      write("START REJECTED - NO SYSTEM SELECTED");
      @sysvar::MasterCtrl::StartTest=0;
      return;
    }

    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);
    cancelTimer(monitorTimer);
    cancelTimer(stopTimer);

    testRunning=1;
    finalStopPending=0;
    step=0;
    cycle=0;

    elapsedSec=0;
    cycleStartSec=0;

    updateMonitor();

    initMessages();

    /* INITIAL OFF, ISOLATION CLOSED */

    setMode(0);
    setIsolation(1);

    send100();
    send500();
    send1000();

    setTimer(t100,100);
    setTimer(t500,500);
    setTimer(t1000,1000);
    setTimer(monitorTimer,1000);

    write("==========================================");
    write("PANEL START - 4 CYCLE 20 HOUR TEST");
    write("CAN1=%d CAN2=%d CAN3=%d",sys1,sys2,sys3);
    write("CAN4=%d CAN5=%d CAN6=%d",sys4,sys5,sys6);
    write("INITIAL OFF - 1 SECOND");
    write("FLOAT 4 HOURS / STANDBY 1 HOUR");
    write("TOTAL DURATION - 20 HOURS + 2 SECONDS");
    write("==========================================");

    setTimer(seqTimer,1000);

    @sysvar::MasterCtrl::StartTest=0;
  }
}
