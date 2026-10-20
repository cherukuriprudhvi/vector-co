


/*@!Encoding:1252*/

variables
{
  /* SYSTEM SELECTION
     0 = NONE
     1 = EBB
     2 = EMB
     3 = 48V EPAS
     4 = 12V EPAS
  */

  int sys1 = 3;

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seqTimer;

  int step = 0;
  int cycle = 0;

  /* RECOVERY CONFIGURATION */

  int resumeMode = 1;
  int resumeCycle = 5;

  /* Remaining FLOAT: 15 hours 15 minutes */
  long resumeFloatMs = 54900000;

  /* CAN1 - BCM6_BCM_CANFD DATABASE */

  message BCM6_BCM_CANFD::BCM_AutoSar_Network_Mgmt bcm1;
  message BCM6_BCM_CANFD::BodyInfo_3 body1;

  message BCM6_BCM_CANFD::DCDCE_AutoSar_Network_Mgmt dcdce1;
  message BCM6_BCM_CANFD::DCDCF_AutoSar_Network_Mgmt dcdcf1;
  message BCM6_BCM_CANFD::DCDCG_AutoSar_Network_Mgmt dcdcg1;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_1 ebbCtrl1;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_1 ebbInfo1;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_2 embCtrl1;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_2 embInfo1;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_3 v48Ctrl1;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_3 v48Info1;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_4 epasCtrl1;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_4 epasInfo1;
}


/* INITIALIZE ALL REQUIRED MESSAGES */

void initMessages()
{
  int i;

  bcm1.CAN = 1;
  body1.CAN = 1;

  dcdce1.CAN = 1;
  dcdcf1.CAN = 1;
  dcdcg1.CAN = 1;

  ebbCtrl1.CAN = 1;
  ebbInfo1.CAN = 1;

  embCtrl1.CAN = 1;
  embInfo1.CAN = 1;

  v48Ctrl1.CAN = 1;
  v48Info1.CAN = 1;

  epasCtrl1.CAN = 1;
  epasInfo1.CAN = 1;

  /* BCM NETWORK MANAGEMENT */

  bcm1.byte(0)=129;
  bcm1.byte(1)=0;

  for(i=2;i<8;i++)
  {
    bcm1.byte(i)=255;
  }

  /* DCDCE NETWORK MANAGEMENT */

  dcdce1.byte(0)=0;
  dcdce1.byte(1)=129;

  for(i=2;i<8;i++)
  {
    dcdce1.byte(i)=255;
  }

  /* DCDCF NETWORK MANAGEMENT */

  dcdcf1.byte(0)=0;
  dcdcf1.byte(1)=129;

  for(i=2;i<8;i++)
  {
    dcdcf1.byte(i)=255;
  }

  /* DCDCG NETWORK MANAGEMENT */

  dcdcg1.byte(0)=0;
  dcdcg1.byte(1)=129;

  for(i=2;i<8;i++)
  {
    dcdcg1.byte(i)=255;
  }

  /* BODY INFO */

  for(i=0;i<8;i++)
  {
    body1.byte(i)=0;
  }

  body1.byte(0)=4;
  body1.byte(3)=12;
  body1.byte(4)=230;

  body1.Parklamp_Status=1;
  body1.Ignition_Status=4;

  /* EBB CONTROL DEFAULTS */

  ebbCtrl1.byte(0)=30;
  ebbCtrl1.byte(1)=168;
  ebbCtrl1.byte(2)=0;
  ebbCtrl1.byte(3)=13;
  ebbCtrl1.byte(4)=52;
  ebbCtrl1.byte(5)=192;
  ebbCtrl1.byte(6)=0;
  ebbCtrl1.byte(7)=0;

  /* EMB CONTROL DEFAULTS */

  embCtrl1.byte(0)=30;
  embCtrl1.byte(1)=168;
  embCtrl1.byte(2)=0;
  embCtrl1.byte(3)=13;
  embCtrl1.byte(4)=52;
  embCtrl1.byte(5)=192;
  embCtrl1.byte(6)=0;
  embCtrl1.byte(7)=0;

  /* 12V EPAS CONTROL DEFAULTS */

  epasCtrl1.byte(0)=30;
  epasCtrl1.byte(1)=168;
  epasCtrl1.byte(2)=0;
  epasCtrl1.byte(3)=13;
  epasCtrl1.byte(4)=52;
  epasCtrl1.byte(5)=192;
  epasCtrl1.byte(6)=0;
  epasCtrl1.byte(7)=0;

  /* 48V EPAS CONTROL DEFAULTS */

  v48Ctrl1.byte(0)=254;
  v48Ctrl1.byte(1)=254;
  v48Ctrl1.byte(2)=254;
  v48Ctrl1.byte(3)=30;
  v48Ctrl1.byte(4)=0;
  v48Ctrl1.byte(5)=0;
  v48Ctrl1.byte(6)=0;
  v48Ctrl1.byte(7)=0;

  /* EBB INFORMATION */

  for(i=0;i<8;i++)
  {
    ebbInfo1.byte(i)=0;
  }

  ebbInfo1.byte(6)=162;
  ebbInfo1.byte(7)=128;

  /* EMB INFORMATION */

  for(i=0;i<8;i++)
  {
    embInfo1.byte(i)=0;
  }

  embInfo1.byte(6)=162;
  embInfo1.byte(7)=128;

  /* 12V EPAS INFORMATION */

  for(i=0;i<8;i++)
  {
    epasInfo1.byte(i)=0;
  }

  epasInfo1.byte(6)=162;
  epasInfo1.byte(7)=128;

  /* 48V EPAS INFORMATION */

  v48Info1.byte(0)=8;
  v48Info1.byte(1)=254;
  v48Info1.byte(2)=254;
  v48Info1.byte(3)=0;
  v48Info1.byte(4)=0;
  v48Info1.byte(5)=0;
  v48Info1.byte(6)=0;
  v48Info1.byte(7)=0;
}


/* SET MODE
   0 = OFF
   1 = STANDBY
   3 = FLOAT
*/

void setMode(int mode)
{
  if(sys1==1)
  {
    ebbCtrl1.EMduleMde_D_Rq=mode;
  }
  else if(sys1==2)
  {
    embCtrl1.EMduleMde_D_Rq2=mode;
  }
  else if(sys1==3)
  {
    v48Ctrl1.UCapMduleMde_D_Rq=mode;
  }
  else if(sys1==4)
  {
    epasCtrl1.EMduleMde_D_Rq3=mode;
  }
}


/* ISOLATION
   0 = OPEN
   1 = CLOSE
   48V EPAS HAS NO ISOLATION
*/

void setIsolation(int value)
{
  if(sys1==1)
  {
    ebbCtrl1.IsolSwtch_B_Cmd=value;
  }
  else if(sys1==2)
  {
    embCtrl1.IsolSwtch_B_Cmd2=value;
  }
  else if(sys1==4)
  {
    epasCtrl1.IsolSwtch_B_Cmd3=value;
  }
}


/* SEND CONTROL AND INFO EVERY 100 MS */

void send100()
{
  if(sys1==1)
  {
    output(ebbCtrl1);
    output(ebbInfo1);
  }
  else if(sys1==2)
  {
    output(embCtrl1);
    output(embInfo1);
  }
  else if(sys1==3)
  {
    output(v48Ctrl1);
    output(v48Info1);
  }
  else if(sys1==4)
  {
    output(epasCtrl1);
    output(epasInfo1);
  }
}


/* SEND BODY INFO EVERY 500 MS */

void send500()
{
  if(sys1!=0)
  {
    output(body1);
  }
}


/* SEND NETWORK MANAGEMENT EVERY 1000 MS */

void send1000()
{
  if(sys1!=0)
  {
    output(bcm1);
  }

  if(sys1==1)
  {
    output(dcdcf1);
    output(dcdcg1);
  }
  else if(sys1==2)
  {
    output(dcdce1);
    output(dcdcf1);
  }
  else if(sys1==3)
  {
    output(dcdce1);
    output(dcdcg1);
  }
  else if(sys1==4)
  {
    output(dcdcg1);
  }
}


/* START MEASUREMENT */

on start
{
  if(sys1<1 || sys1>4)
  {
    write("ERROR: SELECT SYSTEM 1 TO 4");
    return;
  }

  initMessages();

  /* Set up recovery before first control output */

  if(resumeMode==1)
  {
    cycle=resumeCycle;
    step=3;

    setMode(3);
    setIsolation(1);

    write("================================");
    write("FIVE-DAY TEST RECOVERY STARTED");
    write("================================");

    write("SYSTEM SELECTED: %d",sys1);
    write("RESUME CYCLE: %d",cycle);
    write("RESUME PHASE: FLOAT");
    write("FLOAT REMAINING MS: %ld",
          resumeFloatMs);
    write("AFTER FLOAT: STANDBY 6 HOURS");
    write("AFTER STANDBY: FINAL OFF");

    setTimer(seqTimer,resumeFloatMs);
  }
  else
  {
    step=0;
    cycle=0;

    setMode(0);
    setIsolation(1);

    write("CAN1 FIVE-DAY MASTER STARTED");
    write("SYSTEM SELECTED: %d",sys1);
    write("STARTUP OFF - 2 SECONDS");

    setTimer(seqTimer,2000);
  }

  send100();
  send500();
  send1000();

  setTimer(t100,100);
  setTimer(t500,500);
  setTimer(t1000,1000);
}


/* PERIODIC TIMERS */

on timer t100
{
  send100();
  setTimer(t100,100);
}

on timer t500
{
  send500();
  setTimer(t500,500);
}

on timer t1000
{
  send1000();
  setTimer(t1000,1000);
}


/* FIVE-DAY MASTER SEQUENCE */

on timer seqTimer
{
  /* OFF -> STANDBY */

  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("STARTUP STANDBY - 2 SECONDS");

    step=1;
    setTimer(seqTimer,2000);
  }

  /* FIRST FLOAT CYCLE */

  else if(step==1)
  {
    cycle=1;

    setMode(3);

    if(sys1!=3)
    {
      setIsolation(0);
      write("DAY %d: ISOLATION OPEN",cycle);
    }

    write("DAY %d: FLOAT START",cycle);

    step=2;
    setTimer(seqTimer,1000);
  }

  /* CLOSE ISOLATION AND HOLD FLOAT */

  else if(step==2)
  {
    if(sys1!=3)
    {
      setIsolation(1);
      write("DAY %d: ISOLATION CLOSED",cycle);
    }

    write("DAY %d: FLOAT HOLD",cycle);

    step=3;

    /* 18 HOURS MINUS 1 SECOND */
    setTimer(seqTimer,64799000);
  }

  /* FLOAT -> STANDBY */

  else if(step==3)
  {
    setMode(1);
    setIsolation(1);

    write("DAY %d: FLOAT COMPLETE",cycle);
    write("DAY %d: STANDBY - 6 HOURS",cycle);

    step=4;
    setTimer(seqTimer,21600000);
  }

  /* NEXT DAY OR COMPLETE */

  else if(step==4)
  {
    if(cycle>=5)
    {
      setMode(0);
      setIsolation(1);
      send100();

      write("FIVE CYCLES COMPLETE");
      write("RECOVERY SEQUENCE FINISHED");
      write("FINAL OFF - 2 SECONDS");

      step=5;
      setTimer(seqTimer,2000);
    }
    else
    {
      cycle++;

      setMode(3);

      if(sys1!=3)
      {
        setIsolation(0);
        write("DAY %d: ISOLATION OPEN",cycle);
      }

      write("DAY %d: FLOAT START",cycle);

      step=2;
      setTimer(seqTimer,1000);
    }
  }

  /* STOP MEASUREMENT */

  else if(step==5)
  {
    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);

    write("FIVE-DAY RECOVERY COMPLETE");
    write("STOP MEASUREMENT");

    stop();
  }
}

