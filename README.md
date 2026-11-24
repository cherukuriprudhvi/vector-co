
/*@!Encoding:1252*/

/*
 CLARIOS SIX CHANNEL MASTER TEST
 SINGLE CYCLE - 5 MINUTES FLOAT

 SYSTEM SELECTION
 0 = NONE
 1 = EBB
 2 = EMB
 3 = 48V EPAS
 4 = 12V EPAS

 MODE
 0 = SLEEP
 1 = STANDBY
 3 = FLOAT
 4 = CHARGE

 D ISOLATION
 1 = OPEN
 2 = CLOSE

 INDEPENDENT CHANNEL VOLTAGE CONTROL
*/

variables
{
  int sys[6];
  int state[6];
  int channelMode[6];
  int voltageValid[6];

  float cellVoltage[6];

  long stateTicks[6];
  long floatTicks[6];
  long rxAge[6];

  int testRunning=0;
  int finalStopPending=0;
  int stopping=0;
  int cycle=0;

  long elapsedSec=0;
  long totalTicks=0;

  long floatDuration=3000;
  long wakeTimeout=100;
  long feedbackTimeout=20;
  long chargeTimeout=600;

  float voltageThreshold=5.6;

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer stopTimer;

  message CAN1.BCM_AutoSar_Network_Mgmt bcm[6];
  message CAN1.BodyInfo_3 body[6];

  message CAN1.DCDCE_AutoSar_Network_Mgmt dcdce[6];
  message CAN1.DCDCF_AutoSar_Network_Mgmt dcdcf[6];
  message CAN1.DCDCG_AutoSar_Network_Mgmt dcdcg[6];

  message CAN1.EnergyMgmtBodyCtrl_1 ebbCtrl[6];
  message CAN1.EnergyMgmtBodyInfo_1 ebbInfo[6];

  message CAN1.EnergyMgmtBodyCtrl_2 embCtrl[6];
  message CAN1.EnergyMgmtBodyInfo_2 embInfo[6];

  message CAN1.EnergyMgmtBodyCtrl_3 v48Ctrl[6];
  message CAN1.EnergyMgmtBodyInfo_3 v48Info[6];

  message CAN1.EnergyMgmtBodyCtrl_4 epasCtrl[6];
  message CAN1.EnergyMgmtBodyInfo_4 epasInfo[6];
}


/* ========================================
   MESSAGE INITIALIZATION
   ======================================== */

void initMessages()
{
  int i;
  int j;

  for(i=0;i<6;i++)
  {
    /* ASSIGN PHYSICAL CAN CHANNEL */

    bcm[i].CAN=i+1;
    body[i].CAN=i+1;

    dcdce[i].CAN=i+1;
    dcdcf[i].CAN=i+1;
    dcdcg[i].CAN=i+1;

    ebbCtrl[i].CAN=i+1;
    ebbInfo[i].CAN=i+1;

    embCtrl[i].CAN=i+1;
    embInfo[i].CAN=i+1;

    v48Ctrl[i].CAN=i+1;
    v48Info[i].CAN=i+1;

    epasCtrl[i].CAN=i+1;
    epasInfo[i].CAN=i+1;

    /* CAN FD */

    bcm[i].FDF=1;
    bcm[i].BRS=1;

    body[i].FDF=1;
    body[i].BRS=1;

    dcdce[i].FDF=1;
    dcdce[i].BRS=1;

    dcdcf[i].FDF=1;
    dcdcf[i].BRS=1;

    dcdcg[i].FDF=1;
    dcdcg[i].BRS=1;

    ebbCtrl[i].FDF=1;
    ebbCtrl[i].BRS=1;
    ebbInfo[i].FDF=1;
    ebbInfo[i].BRS=1;

    embCtrl[i].FDF=1;
    embCtrl[i].BRS=1;
    embInfo[i].FDF=1;
    embInfo[i].BRS=1;

    v48Ctrl[i].FDF=1;
    v48Ctrl[i].BRS=1;
    v48Info[i].FDF=1;
    v48Info[i].BRS=1;

    epasCtrl[i].FDF=1;
    epasCtrl[i].BRS=1;
    epasInfo[i].FDF=1;
    epasInfo[i].BRS=1;

    /* MESSAGE LENGTH */

    bcm[i].DLC=8;
    body[i].DLC=10;

    dcdce[i].DLC=8;
    dcdcf[i].DLC=8;
    dcdcg[i].DLC=8;

    ebbCtrl[i].DLC=8;
    ebbInfo[i].DLC=8;

    embCtrl[i].DLC=8;
    embInfo[i].DLC=8;

    v48Ctrl[i].DLC=8;
    v48Info[i].DLC=8;

    epasCtrl[i].DLC=8;
    epasInfo[i].DLC=8;

    /* BCM NETWORK MANAGEMENT */

    bcm[i].BCM_AutoSarNMNodeId=129;
    bcm[i].BCM_AutoSarNMControl=0;
    bcm[i].BCM_AutoSarNMReserved1=255;
    bcm[i].BCM_AutoSarNMReserved2=255;
    bcm[i].BCM_GWOnBoardTester=255;
    bcm[i].BCM_GWNMProxy=255;
    bcm[i].BCM_AutoSarNMReserved3=255;
    bcm[i].BCM_AutoSarNMReserved4=255;

    /* DCDCE NETWORK MANAGEMENT */

    dcdce[i].byte(0)=0;
    dcdce[i].byte(1)=129;

    /* DCDCF NETWORK MANAGEMENT */

    dcdcf[i].byte(0)=0;
    dcdcf[i].byte(1)=129;

    /* DCDCG NETWORK MANAGEMENT */

    dcdcg[i].byte(0)=0;
    dcdcg[i].byte(1)=129;

    for(j=2;j<8;j++)
    {
      dcdce[i].byte(j)=255;
      dcdcf[i].byte(j)=255;
      dcdcg[i].byte(j)=255;
    }

    /* BODY INFO */

    body[i].Parklamp_Status=1;
    body[i].Ignition_Status=4;

    /* EBB CONTROL DEFAULTS */

    ebbCtrl[i].byte(0)=30;
    ebbCtrl[i].byte(1)=168;
    ebbCtrl[i].byte(2)=0;
    ebbCtrl[i].byte(3)=13;
    ebbCtrl[i].byte(4)=52;
    ebbCtrl[i].byte(5)=192;
    ebbCtrl[i].byte(6)=0;
    ebbCtrl[i].byte(7)=0;

    ebbCtrl[i].EMduleDistrPath_R_Calc=254;
    ebbCtrl[i].PwBus_U_Rq=3494;
    ebbCtrl[i].DcdcAout_U_Rq=13;

    ebbCtrl[i].EMduleMde_D_Rq=1;
    ebbCtrl[i].IsolSwtch_D_Cmd=2;

    /* EMB CONTROL DEFAULTS */

    embCtrl[i].byte(0)=30;
    embCtrl[i].byte(1)=168;
    embCtrl[i].byte(2)=0;
    embCtrl[i].byte(3)=13;
    embCtrl[i].byte(4)=52;
    embCtrl[i].byte(5)=192;
    embCtrl[i].byte(6)=0;
    embCtrl[i].byte(7)=0;

    embCtrl[i].EMduleDistrPath_R_Calc2=254;
    embCtrl[i].PwBus_U_Rq2=3494;
    embCtrl[i].DcdcAout_U_Rq2=13;

    embCtrl[i].EMduleMde_D_Rq2=1;
    embCtrl[i].IsolSwtch_D_Cmd2=2;

    /* 12V EPAS CONTROL DEFAULTS */

    epasCtrl[i].byte(0)=30;
    epasCtrl[i].byte(1)=168;
    epasCtrl[i].byte(2)=0;
    epasCtrl[i].byte(3)=13;
    epasCtrl[i].byte(4)=52;
    epasCtrl[i].byte(5)=192;
    epasCtrl[i].byte(6)=0;
    epasCtrl[i].byte(7)=0;

    epasCtrl[i].EMduleDistrPath_R_Calc3=254;
    epasCtrl[i].PwBus_U_Rq3=3494;
    epasCtrl[i].DcdcAout_U_Rq3=13;

    epasCtrl[i].EMduleMde_D_Rq3=1;
    epasCtrl[i].IsolSwtch_D_Cmd3=2;

    /* 48V EPAS CONTROL DEFAULTS */

    v48Ctrl[i].byte(0)=254;
    v48Ctrl[i].byte(1)=254;
    v48Ctrl[i].byte(2)=254;
    v48Ctrl[i].byte(3)=30;
    v48Ctrl[i].byte(4)=0;
    v48Ctrl[i].byte(5)=0;
    v48Ctrl[i].byte(6)=0;
    v48Ctrl[i].byte(7)=0;

    v48Ctrl[i].UCapMduleMde_D_Rq=1;

    /* INFO DEFAULTS */

    for(j=0;j<8;j++)
    {
      ebbInfo[i].byte(j)=0;
      embInfo[i].byte(j)=0;
      epasInfo[i].byte(j)=0;
      v48Info[i].byte(j)=0;
    }

    /* EBB INFO */

    ebbInfo[i].byte(6)=162;
    ebbInfo[i].byte(7)=128;

    ebbInfo[i].EMduleChrg_I_Mx=4;
    ebbInfo[i].EMduleDchrg_I_Mx=4;

    /* EMB INFO */

    embInfo[i].byte(6)=162;
    embInfo[i].byte(7)=128;

    embInfo[i].EMduleRgen_I_Actl2=0;
    embInfo[i].EMduleBst_I_Actl2=0;
    embInfo[i].EMduleRgen_As_Rsrv2=0;
    embInfo[i].EMduleBst_As_Rsrv2=0;

    embInfo[i].EMduleChrg_I_Mx2=4;
    embInfo[i].EMduleDchrg_I_Mx2=4;

    /* 12V EPAS INFO */

    epasInfo[i].byte(6)=162;
    epasInfo[i].byte(7)=128;

    epasInfo[i].EMduleChrg_I_Mx3=4;
    epasInfo[i].EMduleDchrg_I_Mx3=4;

    /* 48V EPAS INFO */

    v48Info[i].byte(0)=254;
    v48Info[i].byte(1)=254;
    v48Info[i].byte(2)=254;
  }
}


/* ========================================
   INDEPENDENT CHANNEL MODE CONTROL
   ======================================== */

void setChannelMode(int i,int mode)
{
  channelMode[i]=mode;

  if(sys[i]==1)
  {
    ebbCtrl[i].EMduleMde_D_Rq=mode;
    ebbCtrl[i].IsolSwtch_D_Cmd=2;
  }

  else if(sys[i]==2)
  {
    embCtrl[i].EMduleMde_D_Rq2=mode;
    embCtrl[i].IsolSwtch_D_Cmd2=2;
  }

  else if(sys[i]==3)
  {
    v48Ctrl[i].UCapMduleMde_D_Rq=mode;
  }

  else if(sys[i]==4)
  {
    epasCtrl[i].EMduleMde_D_Rq3=mode;
    epasCtrl[i].IsolSwtch_D_Cmd3=2;
  }
}


/* ========================================
   100 MS TRANSMISSION
   ======================================== */

void send100()
{
  int i;

  for(i=0;i<6;i++)
  {
    if(sys[i]==1)
    {
      output(ebbCtrl[i]);
      output(ebbInfo[i]);
    }

    else if(sys[i]==2)
    {
      output(embCtrl[i]);
      output(embInfo[i]);
    }

    else if(sys[i]==3)
    {
      output(v48Ctrl[i]);
      output(v48Info[i]);
    }

    else if(sys[i]==4)
    {
      output(epasCtrl[i]);
      output(epasInfo[i]);
    }
  }
}


/* ========================================
   500 MS TRANSMISSION
   ======================================== */

void send500()
{
  int i;

  for(i=0;i<6;i++)
  {
    if(sys[i]!=0)
    {
      output(body[i]);
    }
  }
}


/* ========================================
   1000 MS TRANSMISSION
   ======================================== */

void send1000()
{
  int i;

  for(i=0;i<6;i++)
  {
    if(sys[i]==1)
    {
      output(bcm[i]);
      output(dcdcf[i]);
      output(dcdcg[i]);
    }

    else if(sys[i]==2)
    {
      output(dcdce[i]);
      output(dcdcf[i]);
    }

    else if(sys[i]==3)
    {
      output(bcm[i]);
      output(dcdce[i]);
      output(dcdcg[i]);
    }

    else if(sys[i]==4)
    {
      output(bcm[i]);
      output(dcdce[i]);
      output(dcdcg[i]);
    }
  }
}


/* ========================================
   VOLTAGE FEEDBACK VALIDATION
   ======================================== */

void receiveVoltage(int i,int moduleType,
                    float voltage)
{
  if(!testRunning || stopping)
    return;

  if(i<0 || i>=6)
    return;

  if(sys[i]!=moduleType)
    return;

  if(state[i]<1 || state[i]>3)
    return;

  /* PROVISIONAL VALIDITY RANGE */

  if(voltage<0.0 || voltage>=15.96875)
  {
    voltageValid[i]=0;
    return;
  }

  cellVoltage[i]=voltage;
  voltageValid[i]=1;
  rxAge[i]=0;
}


/* ========================================
   CAN1 VOLTAGE FEEDBACK
   ======================================== */

on message CAN1.BatteryCellData_1
{
  if(this.dir==rx)
    receiveVoltage(0,1,this.Cell_U_Actl.phys);
}

on message CAN1.BatteryCellData_2
{
  if(this.dir==rx)
    receiveVoltage(0,2,this.Cell_U_Actl2.phys);
}

on message CAN1.BatteryCellData_3
{
  if(this.dir==rx)
  {
    if(sys[0]==3)
      receiveVoltage(0,3,this.Cell_U_Actl3.phys);

    else if(sys[0]==4)
      receiveVoltage(0,4,this.Cell_U_Actl3.phys);
  }
}


/* ========================================
   CAN2 VOLTAGE FEEDBACK
   ======================================== */

on message CAN2.BatteryCellData_1
{
  if(this.dir==rx)
    receiveVoltage(1,1,this.Cell_U_Actl.phys);
}

on message CAN2.BatteryCellData_2
{
  if(this.dir==rx)
    receiveVoltage(1,2,this.Cell_U_Actl2.phys);
}

on message CAN2.BatteryCellData_3
{
  if(this.dir==rx)
  {
    if(sys[1]==3)
      receiveVoltage(1,3,this.Cell_U_Actl3.phys);

    else if(sys[1]==4)
      receiveVoltage(1,4,this.Cell_U_Actl3.phys);
  }
}


/* ========================================
   CAN3 VOLTAGE FEEDBACK
   ======================================== */

on message CAN3.BatteryCellData_1
{
  if(this.dir==rx)
    receiveVoltage(2,1,this.Cell_U_Actl.phys);
}

on message CAN3.BatteryCellData_2
{
  if(this.dir==rx)
    receiveVoltage(2,2,this.Cell_U_Actl2.phys);
}

on message CAN3.BatteryCellData_3
{
  if(this.dir==rx)
  {
    if(sys[2]==3)
      receiveVoltage(2,3,this.Cell_U_Actl3.phys);

    else if(sys[2]==4)
      receiveVoltage(2,4,this.Cell_U_Actl3.phys);
  }
}


/* ========================================
   CAN4 VOLTAGE FEEDBACK
   ======================================== */

on message CAN4.BatteryCellData_1
{
  if(this.dir==rx)
    receiveVoltage(3,1,this.Cell_U_Actl.phys);
}

on message CAN4.BatteryCellData_2
{
  if(this.dir==rx)
    receiveVoltage(3,2,this.Cell_U_Actl2.phys);
}

on message CAN4.BatteryCellData_3
{
  if(this.dir==rx)
  {
    if(sys[3]==3)
      receiveVoltage(3,3,this.Cell_U_Actl3.phys);

    else if(sys[3]==4)
      receiveVoltage(3,4,this.Cell_U_Actl3.phys);
  }
}


/* ========================================
   CAN5 VOLTAGE FEEDBACK
   ======================================== */

on message CAN5.BatteryCellData_1
{
  if(this.dir==rx)
    receiveVoltage(4,1,this.Cell_U_Actl.phys);
}

on message CAN5.BatteryCellData_2
{
  if(this.dir==rx)
    receiveVoltage(4,2,this.Cell_U_Actl2.phys);
}

on message CAN5.BatteryCellData_3
{
  if(this.dir==rx)
  {
    if(sys[4]==3)
      receiveVoltage(4,3,this.Cell_U_Actl3.phys);

    else if(sys[4]==4)
      receiveVoltage(4,4,this.Cell_U_Actl3.phys);
  }
}


/* ========================================
   CAN6 VOLTAGE FEEDBACK
   ======================================== */

on message CAN6.BatteryCellData_1
{
  if(this.dir==rx)
    receiveVoltage(5,1,this.Cell_U_Actl.phys);
}

on message CAN6.BatteryCellData_2
{
  if(this.dir==rx)
    receiveVoltage(5,2,this.Cell_U_Actl2.phys);
}

on message CAN6.BatteryCellData_3
{
  if(this.dir==rx)
  {
    if(sys[5]==3)
      receiveVoltage(5,3,this.Cell_U_Actl3.phys);

    else if(sys[5]==4)
      receiveVoltage(5,4,this.Cell_U_Actl3.phys);
  }
}


/* ========================================
   PANEL MONITOR
   ======================================== */

void updateMonitor()
{
  int i;
  int waiting;
  long remaining;
  long channelRemaining;
  long cycleElapsed;

  char remainingText[32];
  char totalText[32];
  char cycleText[32];

  remaining=0;
  waiting=0;
  cycleElapsed=300;

  for(i=0;i<6;i++)
  {
    if(sys[i]==0)
      continue;

    if(state[i]==1 || state[i]==2)
      waiting=1;

    if(state[i]==3)
    {
      channelRemaining=
        (floatDuration-floatTicks[i]+9)/10;

      if(channelRemaining>remaining)
        remaining=channelRemaining;
    }

    if(floatTicks[i]/10<cycleElapsed)
      cycleElapsed=floatTicks[i]/10;
  }

  if(cycle==0)
    cycleElapsed=0;

  if(waiting)
  {
    remaining=-1;

    snprintf(remainingText,
             elcount(remainingText),
             "WAITING / CHARGING");
  }
  else
  {
    snprintf(remainingText,
             elcount(remainingText),
             "%02d:%02d:%02d",
             remaining/3600,
             (remaining%3600)/60,
             remaining%60);
  }

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
  @sysvar::TestMonitor::TotalElapsedSec=elapsedSec;

  if(remaining<0)
    @sysvar::TestMonitor::RemainingSec=0;
  else
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


/* ========================================
   START FLOAT ON INDIVIDUAL CHANNEL
   ======================================== */

void startFloat(int i)
{
  state[i]=3;
  stateTicks[i]=0;
  floatTicks[i]=0;

  setChannelMode(i,3);

  write("CAN%d FLOAT START - VOLTAGE %.3f V",
        i+1,cellVoltage[i]);

  write("CAN%d FLOAT DURATION = 300 SECONDS",
        i+1);
}


/* ========================================
   CHANNEL SHUTDOWN
   ======================================== */

void finishChannel(int i)
{
  state[i]=4;
  stateTicks[i]=0;

  setChannelMode(i,1);

  write("CAN%d FINAL STANDBY",i+1);
}


/* ========================================
   STOP ALL CHANNELS
   ======================================== */

void requestStop()
{
  int i;

  stopping=1;

  for(i=0;i<6;i++)
  {
    if(sys[i]!=0 && state[i]!=6)
    {
      finishChannel(i);
    }
  }
}


/* ========================================
   INDEPENDENT CHANNEL STATE MACHINE

   0 = DISABLED
   1 = INITIAL STANDBY
   2 = CHARGING
   3 = FLOAT
   4 = FINAL STANDBY
   5 = SLEEP
   6 = COMPLETE
   ======================================== */

void processChannel(int i)
{
  if(sys[i]==0)
    return;

  if(state[i]==6)
    return;

  stateTicks[i]++;
  rxAge[i]++;

  /* INITIAL STANDBY */

  if(state[i]==1)
  {
    if(stateTicks[i]>=10 &&
       voltageValid[i] &&
       rxAge[i]<feedbackTimeout)
    {
      if(cellVoltage[i]<voltageThreshold)
      {
        state[i]=2;
        stateTicks[i]=0;

        setChannelMode(i,4);

        write("CAN%d CHARGE START - %.3f V",
              i+1,cellVoltage[i]);
      }
      else
      {
        startFloat(i);
      }
    }

    else if(stateTicks[i]>=wakeTimeout)
    {
      write("CAN%d FAULT - NO VALID VOLTAGE",
            i+1);

      requestStop();
    }
  }

  /* CHARGING */

  else if(state[i]==2)
  {
    if(!voltageValid[i] ||
       rxAge[i]>=feedbackTimeout)
    {
      write("CAN%d FAULT - VOLTAGE FEEDBACK LOST",
            i+1);

      requestStop();
    }

    else if(stateTicks[i]>=chargeTimeout)
    {
      write("CAN%d FAULT - CHARGE TIMEOUT",
            i+1);

      requestStop();
    }

    else if(cellVoltage[i]>=voltageThreshold)
    {
      write("CAN%d CHARGE COMPLETE - %.3f V",
            i+1,cellVoltage[i]);

      startFloat(i);
    }
  }

  /* FLOAT - 5 MINUTES */

  else if(state[i]==3)
  {
    if(!voltageValid[i] ||
       rxAge[i]>=feedbackTimeout)
    {
      write("CAN%d FAULT - FLOAT FEEDBACK LOST",
            i+1);

      requestStop();
    }

    else if(cellVoltage[i]<voltageThreshold)
    {
      write("CAN%d FAULT - VOLTAGE BELOW THRESHOLD",
            i+1);

      requestStop();
    }

    else
    {
      floatTicks[i]++;

      if(floatTicks[i]>=floatDuration)
      {
        write("CAN%d FIVE MINUTE FLOAT COMPLETE",
              i+1);

        finishChannel(i);
      }
    }
  }

  /* FINAL STANDBY - 1 SECOND */

  else if(state[i]==4)
  {
    if(stateTicks[i]>=10)
    {
      setChannelMode(i,0);

      state[i]=5;
      stateTicks[i]=0;

      write("CAN%d SLEEP",i+1);
    }
  }

  /* FINAL SLEEP - 500 MS */

  else if(state[i]==5)
  {
    if(stateTicks[i]>=5)
    {
      state[i]=6;

      write("CAN%d SEQUENCE COMPLETE",i+1);
    }
  }
}


/* ========================================
   CHECK ALL CHANNELS COMPLETE
   ======================================== */

void checkCompletion()
{
  int i;
  int allComplete;

  allComplete=1;

  for(i=0;i<6;i++)
  {
    if(sys[i]!=0 && state[i]!=6)
      allComplete=0;
  }

  if(allComplete)
  {
    updateMonitor();

    testRunning=0;
    finalStopPending=1;

    cancelTimer(t500);
    cancelTimer(t1000);

    if(stopping)
      write("TEST STOPPED OR ABORTED");
    else
      write("ALL SELECTED CHANNELS COMPLETE");

    write("STOPPING MEASUREMENT AND LOGGING");

    setTimer(stopTimer,100);
  }
}


/* ========================================
   MEASUREMENT START
   ======================================== */

on start
{
  int i;

  testRunning=0;
  finalStopPending=0;
  stopping=0;
  cycle=0;
  elapsedSec=0;
  totalTicks=0;

  for(i=0;i<6;i++)
  {
    sys[i]=0;
    state[i]=0;
    channelMode[i]=0;

    cellVoltage[i]=0.0;
    voltageValid[i]=0;

    stateTicks[i]=0;
    floatTicks[i]=0;
    rxAge[i]=0;
  }

  cancelTimer(t100);
  cancelTimer(t500);
  cancelTimer(t1000);
  cancelTimer(stopTimer);

  @sysvar::MasterCtrl::StartTest=0;
  @sysvar::MasterCtrl::StopTest=0;

  updateMonitor();

  write("MEASUREMENT STARTED");
  write("WAITING FOR PANEL START");
}


/* ========================================
   PANEL START BUTTON
   ======================================== */

on sysvar MasterCtrl::StartTest
{
  int i;
  int selected;

  if(@this==1 &&
     !testRunning &&
     !finalStopPending)
  {
    sys[0]=@sysvar::CH1::Module;
    sys[1]=@sysvar::CH2::Module;
    sys[2]=@sysvar::CH3::Module;
    sys[3]=@sysvar::CH4::Module;
    sys[4]=@sysvar::CH5::Module;
    sys[5]=@sysvar::CH6::Module;

    selected=0;

    for(i=0;i<6;i++)
    {
      if(sys[i]<0 || sys[i]>4)
      {
        write("CAN%d INVALID MODULE SELECTION",
              i+1);

        @sysvar::MasterCtrl::StartTest=0;
        return;
      }

      if(sys[i]!=0)
        selected++;
    }

    if(selected==0)
    {
      write("START REJECTED - NO MODULE SELECTED");

      @sysvar::MasterCtrl::StartTest=0;
      return;
    }

    initMessages();

    testRunning=1;
    finalStopPending=0;
    stopping=0;

    cycle=1;
    elapsedSec=0;
    totalTicks=0;

    for(i=0;i<6;i++)
    {
      state[i]=0;
      stateTicks[i]=0;
      floatTicks[i]=0;

      cellVoltage[i]=0.0;
      voltageValid[i]=0;
      rxAge[i]=0;

      if(sys[i]!=0)
      {
        state[i]=1;

        setChannelMode(i,1);

        write("CAN%d SYSTEM %d - STANDBY",
              i+1,sys[i]);
      }
    }

    /* START ALL LOGGING BLOCKS */

    trigger();

    write("CAPL LOGGING TRIGGER SENT");

    send500();
    send1000();
    send100();

    updateMonitor();

    setTimer(t100,100);
    setTimer(t500,500);
    setTimer(t1000,1000);

    write("SINGLE CYCLE TEST STARTED");
    write("FLOAT DURATION = 5 MINUTES");

    @sysvar::MasterCtrl::StartTest=0;
  }
}


/* ========================================
   PANEL STOP BUTTON
   ======================================== */

on sysvar MasterCtrl::StopTest
{
  if(@this==1)
  {
    if(testRunning && !stopping)
    {
      write("MANUAL STOP REQUESTED");

      requestStop();
      send100();
    }

    @sysvar::MasterCtrl::StopTest=0;
  }
}


/* ========================================
   100 MS MASTER TIMER
   ======================================== */

on timer t100
{
  int i;

  if(testRunning)
  {
    totalTicks++;
    elapsedSec=totalTicks/10;

    for(i=0;i<6;i++)
    {
      processChannel(i);
    }

    send100();

    if(totalTicks%10==0)
      updateMonitor();

    checkCompletion();

    if(testRunning)
      setTimer(t100,100);
  }
}


/* ========================================
   500 MS TIMER
   ======================================== */

on timer t500
{
  if(testRunning)
  {
    send500();
    setTimer(t500,500);
  }
}


/* ========================================
   1000 MS TIMER
   ======================================== */

on timer t1000
{
  if(testRunning)
  {
    send1000();
    setTimer(t1000,1000);
  }
}


/* ========================================
   AUTOMATIC MEASUREMENT STOP
   ======================================== */

on timer stopTimer
{
  if(finalStopPending)
  {
    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);

    finalStopPending=0;

    write("MEASUREMENT STOP");
    write("ALL BLF LOGGING BLOCKS STOP");

    stop();
  }
}