


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

  int sys1 = 1;  // CAN1 EBB
  int sys2 = 1;  // CAN2 EBB

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seqTimer;

  int step = 0;

  /* SAME DATABASE - SEPARATE MESSAGE OBJECTS */

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

  message BCM6_BCM_CANFD::BCM_AutoSar_Network_Mgmt bcm2;
  message BCM6_BCM_CANFD::BodyInfo_3 body2;
  message BCM6_BCM_CANFD::DCDCE_AutoSar_Network_Mgmt dcdce2;
  message BCM6_BCM_CANFD::DCDCF_AutoSar_Network_Mgmt dcdcf2;
  message BCM6_BCM_CANFD::DCDCG_AutoSar_Network_Mgmt dcdcg2;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_1 ebbCtrl2;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_1 ebbInfo2;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_2 embCtrl2;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_2 embInfo2;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_3 v48Ctrl2;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_3 v48Info2;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_4 epasCtrl2;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_4 epasInfo2;
}


/* INITIALIZE MESSAGES */

void initMessages()
{
  int i;

  /* PHYSICAL CHANNEL ROUTING */

  bcm1.CAN=1;
  body1.CAN=1;
  dcdce1.CAN=1;
  dcdcf1.CAN=1;
  dcdcg1.CAN=1;
  ebbCtrl1.CAN=1;
  ebbInfo1.CAN=1;
  embCtrl1.CAN=1;
  embInfo1.CAN=1;
  v48Ctrl1.CAN=1;
  v48Info1.CAN=1;
  epasCtrl1.CAN=1;
  epasInfo1.CAN=1;

  bcm2.CAN=2;
  body2.CAN=2;
  dcdce2.CAN=2;
  dcdcf2.CAN=2;
  dcdcg2.CAN=2;
  ebbCtrl2.CAN=2;
  ebbInfo2.CAN=2;
  embCtrl2.CAN=2;
  embInfo2.CAN=2;
  v48Ctrl2.CAN=2;
  v48Info2.CAN=2;
  epasCtrl2.CAN=2;
  epasInfo2.CAN=2;

  /* NETWORK MANAGEMENT PAYLOADS */

  bcm1.byte(0)=129;
  bcm1.byte(1)=0;

  dcdce1.byte(0)=0;
  dcdce1.byte(1)=129;

  dcdcf1.byte(0)=0;
  dcdcf1.byte(1)=129;

  dcdcg1.byte(0)=0;
  dcdcg1.byte(1)=129;

  for(i=2;i<8;i++)
  {
    bcm1.byte(i)=255;
    dcdce1.byte(i)=255;
    dcdcf1.byte(i)=255;
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

  /* CONTROL DEFAULTS */

  for(i=0;i<8;i++)
  {
    ebbCtrl1.byte(i)=0;
    embCtrl1.byte(i)=0;
    epasCtrl1.byte(i)=0;
    v48Ctrl1.byte(i)=0;
  }

  ebbCtrl1.byte(0)=30;
  ebbCtrl1.byte(1)=168;
  ebbCtrl1.byte(3)=13;
  ebbCtrl1.byte(4)=52;
  ebbCtrl1.byte(5)=192;

  embCtrl1.byte(0)=30;
  embCtrl1.byte(1)=168;
  embCtrl1.byte(3)=13;
  embCtrl1.byte(4)=52;
  embCtrl1.byte(5)=192;

  epasCtrl1.byte(0)=30;
  epasCtrl1.byte(1)=168;
  epasCtrl1.byte(3)=13;
  epasCtrl1.byte(4)=52;
  epasCtrl1.byte(5)=192;

  v48Ctrl1.byte(0)=254;
  v48Ctrl1.byte(1)=254;
  v48Ctrl1.byte(2)=254;
  v48Ctrl1.byte(3)=30;

  /* INFO DEFAULTS */

  for(i=0;i<8;i++)
  {
    ebbInfo1.byte(i)=0;
    embInfo1.byte(i)=0;
    epasInfo1.byte(i)=0;
    v48Info1.byte(i)=0;
  }

  ebbInfo1.byte(6)=162;
  ebbInfo1.byte(7)=128;

  embInfo1.byte(6)=162;
  embInfo1.byte(7)=128;

  epasInfo1.byte(6)=162;
  epasInfo1.byte(7)=128;

  v48Info1.byte(0)=8;
  v48Info1.byte(1)=254;
  v48Info1.byte(2)=254;

  /* COPY INITIALIZED PAYLOADS TO CAN2 */

  bcm2=bcm1;
  body2=body1;

  dcdce2=dcdce1;
  dcdcf2=dcdcf1;
  dcdcg2=dcdcg1;

  ebbCtrl2=ebbCtrl1;
  ebbInfo2=ebbInfo1;

  embCtrl2=embCtrl1;
  embInfo2=embInfo1;

  v48Ctrl2=v48Ctrl1;
  v48Info2=v48Info1;

  epasCtrl2=epasCtrl1;
  epasInfo2=epasInfo1;

  /* REAPPLY CAN2 ROUTING AFTER COPYING */

  bcm2.CAN=2;
  body2.CAN=2;
  dcdce2.CAN=2;
  dcdcf2.CAN=2;
  dcdcg2.CAN=2;

  ebbCtrl2.CAN=2;
  ebbInfo2.CAN=2;
  embCtrl2.CAN=2;
  embInfo2.CAN=2;
  v48Ctrl2.CAN=2;
  v48Info2.CAN=2;
  epasCtrl2.CAN=2;
  epasInfo2.CAN=2;
}


/* SET MODE ON BOTH CHANNELS */

void setMode(int mode)
{
  if(sys1==1) ebbCtrl1.EMduleMde_D_Rq=mode;
  else if(sys1==2) embCtrl1.EMduleMde_D_Rq2=mode;
  else if(sys1==3) v48Ctrl1.UCapMduleMde_D_Rq=mode;
  else if(sys1==4) epasCtrl1.EMduleMde_D_Rq3=mode;

  if(sys2==1) ebbCtrl2.EMduleMde_D_Rq=mode;
  else if(sys2==2) embCtrl2.EMduleMde_D_Rq2=mode;
  else if(sys2==3) v48Ctrl2.UCapMduleMde_D_Rq=mode;
  else if(sys2==4) epasCtrl2.EMduleMde_D_Rq3=mode;
}


/* ISOLATION ON BOTH CHANNELS */

void setIsolation(int value)
{
  if(sys1==1) ebbCtrl1.IsolSwtch_B_Cmd=value;
  else if(sys1==2) embCtrl1.IsolSwtch_B_Cmd2=value;
  else if(sys1==4) epasCtrl1.IsolSwtch_B_Cmd3=value;

  if(sys2==1) ebbCtrl2.IsolSwtch_B_Cmd=value;
  else if(sys2==2) embCtrl2.IsolSwtch_B_Cmd2=value;
  else if(sys2==4) epasCtrl2.IsolSwtch_B_Cmd3=value;
}


/* CONTROL + INFO EVERY 100 MS */

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

  if(sys2==1)
  {
    output(ebbCtrl2);
    output(ebbInfo2);
  }
  else if(sys2==2)
  {
    output(embCtrl2);
    output(embInfo2);
  }
  else if(sys2==3)
  {
    output(v48Ctrl2);
    output(v48Info2);
  }
  else if(sys2==4)
  {
    output(epasCtrl2);
    output(epasInfo2);
  }
}


/* BODY INFO EVERY 500 MS */

void send500()
{
  if(sys1!=0) output(body1);
  if(sys2!=0) output(body2);
}


/* NETWORK MANAGEMENT EVERY 1000 MS */

void send1000()
{
  if(sys1!=0) output(bcm1);

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

  if(sys2!=0) output(bcm2);

  if(sys2==1)
  {
    output(dcdcf2);
    output(dcdcg2);
  }
  else if(sys2==2)
  {
    output(dcdce2);
    output(dcdcf2);
  }
  else if(sys2==3)
  {
    output(dcdce2);
    output(dcdcg2);
  }
  else if(sys2==4)
  {
    output(dcdcg2);
  }
}


/* START */

on start
{
  if(sys1<0 || sys1>4 || sys2<0 || sys2>4 ||
     (sys1==0 && sys2==0))
  {
    write("ERROR: INVALID SYSTEM SELECTION");
    return;
  }

  initMessages();

  step=0;

  setMode(0);
  setIsolation(1);

  send100();
  send500();
  send1000();

  setTimer(t100,100);
  setTimer(t500,500);
  setTimer(t1000,1000);

  write("TWO-CHANNEL TEST STARTED");
  write("CAN1 SYSTEM: %d",sys1);
  write("CAN2 SYSTEM: %d",sys2);
  write("OFF - 1 SECOND");

  setTimer(seqTimer,1000);
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


/* TWO-MINUTE TEST SEQUENCE */

on timer seqTimer
{
  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("BOTH CHANNELS: STANDBY - 1 SECOND");

    step=1;
    setTimer(seqTimer,1000);
  }

  else if(step==1)
  {
    setMode(3);
    setIsolation(1);

    write("BOTH CHANNELS: FLOAT - 1 SECOND");

    step=2;
    setTimer(seqTimer,1000);
  }

  else if(step==2)
  {
    setIsolation(0);

    write("BOTH CHANNELS: ISOLATION OPEN - 1 SECOND");

    step=3;
    setTimer(seqTimer,1000);
  }

  else if(step==3)
  {
    setIsolation(1);

    write("BOTH CHANNELS: ISOLATION CLOSED");

    step=4;
    setTimer(seqTimer,1000);
  }

  else if(step==4)
  {
    write("BOTH CHANNELS: FLOAT HOLD - 2 MINUTES");

    step=5;
    setTimer(seqTimer,120000);
  }

  else if(step==5)
  {
    setMode(1);
    setIsolation(1);

    write("BOTH CHANNELS: STANDBY - 1 SECOND");

    step=6;
    setTimer(seqTimer,1000);
  }

  else if(step==6)
  {
    setMode(0);
    setIsolation(1);

    send100();

    write("BOTH CHANNELS: OFF - 1 SECOND");

    step=7;
    setTimer(seqTimer,1000);
  }

  else if(step==7)
  {
    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);

    write("TWO-CHANNEL TWO-MINUTE TEST COMPLETE");

    stop();
  }
}
