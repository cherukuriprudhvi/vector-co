


/*@!Encoding:1252*/

/*
  HUMIDITY TEST - SHORT VALIDATION
  CANalyzer 16 SP8

  SYSTEM SELECTION:
  0 = NONE
  1 = EBB
  2 = EMB
  3 = 48V EPAS
  4 = 12V EPAS

  STARTUP:
  OFF       2 seconds
  STANDBY   2 seconds

  EACH CYCLE:
  FLOAT     5 seconds
    Isolation OPEN for first 1 second
    Isolation CLOSE for remaining 4 seconds
  STANDBY   2 seconds

  TOTAL: 2 CYCLES / 18 SECONDS

  48V EPAS: NO ISOLATION COMMAND

  EXISTING PANEL VARIABLES ONLY:
  CH1::Module ... CH6::Module
  MasterCtrl::StartTest
  MasterCtrl::StopTest
*/

variables
{
  int sys1=0;
  int sys2=0;
  int sys3=0;
  int sys4=0;
  int sys5=0;
  int sys6=0;

  int testRunning=0;
  int step=0;
  int cycle=0;

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seqTimer;

  /* CAN1 */

  message CAN1.BCM_AutoSar_Network_Mgmt bcm1;
  message CAN1.BodyInfo_3 body1;
  message CAN1.DCDCE_AutoSar_Network_Mgmt dcdce1;
  message CAN1.DCDCF_AutoSar_Network_Mgmt dcdcf1;
  message CAN1.DCDCG_AutoSar_Network_Mgmt dcdcg1;

  message CAN1.EnergyMgmtBodyCtrl_1 ebbCtrl1;
  message CAN1.EnergyMgmtBodyInfo_1 ebbInfo1;
  message CAN1.EnergyMgmtBodyCtrl_2 embCtrl1;
  message CAN1.EnergyMgmtBodyInfo_2 embInfo1;
  message CAN1.EnergyMgmtBodyCtrl_3 v48Ctrl1;
  message CAN1.EnergyMgmtBodyInfo_3 v48Info1;
  message CAN1.EnergyMgmtBodyCtrl_4 epasCtrl1;
  message CAN1.EnergyMgmtBodyInfo_4 epasInfo1;

  /* CAN2 */

  message CAN2.BCM_AutoSar_Network_Mgmt bcm2;
  message CAN2.BodyInfo_3 body2;
  message CAN2.DCDCE_AutoSar_Network_Mgmt dcdce2;
  message CAN2.DCDCF_AutoSar_Network_Mgmt dcdcf2;
  message CAN2.DCDCG_AutoSar_Network_Mgmt dcdcg2;

  message CAN2.EnergyMgmtBodyCtrl_1 ebbCtrl2;
  message CAN2.EnergyMgmtBodyInfo_1 ebbInfo2;
  message CAN2.EnergyMgmtBodyCtrl_2 embCtrl2;
  message CAN2.EnergyMgmtBodyInfo_2 embInfo2;
  message CAN2.EnergyMgmtBodyCtrl_3 v48Ctrl2;
  message CAN2.EnergyMgmtBodyInfo_3 v48Info2;
  message CAN2.EnergyMgmtBodyCtrl_4 epasCtrl2;
  message CAN2.EnergyMgmtBodyInfo_4 epasInfo2;

  /* CAN3 */

  message CAN3.BCM_AutoSar_Network_Mgmt bcm3;
  message CAN3.BodyInfo_3 body3;
  message CAN3.DCDCE_AutoSar_Network_Mgmt dcdce3;
  message CAN3.DCDCF_AutoSar_Network_Mgmt dcdcf3;
  message CAN3.DCDCG_AutoSar_Network_Mgmt dcdcg3;

  message CAN3.EnergyMgmtBodyCtrl_1 ebbCtrl3;
  message CAN3.EnergyMgmtBodyInfo_1 ebbInfo3;
  message CAN3.EnergyMgmtBodyCtrl_2 embCtrl3;
  message CAN3.EnergyMgmtBodyInfo_2 embInfo3;
  message CAN3.EnergyMgmtBodyCtrl_3 v48Ctrl3;
  message CAN3.EnergyMgmtBodyInfo_3 v48Info3;
  message CAN3.EnergyMgmtBodyCtrl_4 epasCtrl3;
  message CAN3.EnergyMgmtBodyInfo_4 epasInfo3;

  /* CAN4 */

  message CAN4.BCM_AutoSar_Network_Mgmt bcm4;
  message CAN4.BodyInfo_3 body4;
  message CAN4.DCDCE_AutoSar_Network_Mgmt dcdce4;
  message CAN4.DCDCF_AutoSar_Network_Mgmt dcdcf4;
  message CAN4.DCDCG_AutoSar_Network_Mgmt dcdcg4;

  message CAN4.EnergyMgmtBodyCtrl_1 ebbCtrl4;
  message CAN4.EnergyMgmtBodyInfo_1 ebbInfo4;
  message CAN4.EnergyMgmtBodyCtrl_2 embCtrl4;
  message CAN4.EnergyMgmtBodyInfo_2 embInfo4;
  message CAN4.EnergyMgmtBodyCtrl_3 v48Ctrl4;
  message CAN4.EnergyMgmtBodyInfo_3 v48Info4;
  message CAN4.EnergyMgmtBodyCtrl_4 epasCtrl4;
  message CAN4.EnergyMgmtBodyInfo_4 epasInfo4;

  /* CAN5 */

  message CAN5.BCM_AutoSar_Network_Mgmt bcm5;
  message CAN5.BodyInfo_3 body5;
  message CAN5.DCDCE_AutoSar_Network_Mgmt dcdce5;
  message CAN5.DCDCF_AutoSar_Network_Mgmt dcdcf5;
  message CAN5.DCDCG_AutoSar_Network_Mgmt dcdcg5;

  message CAN5.EnergyMgmtBodyCtrl_1 ebbCtrl5;
  message CAN5.EnergyMgmtBodyInfo_1 ebbInfo5;
  message CAN5.EnergyMgmtBodyCtrl_2 embCtrl5;
  message CAN5.EnergyMgmtBodyInfo_2 embInfo5;
  message CAN5.EnergyMgmtBodyCtrl_3 v48Ctrl5;
  message CAN5.EnergyMgmtBodyInfo_3 v48Info5;
  message CAN5.EnergyMgmtBodyCtrl_4 epasCtrl5;
  message CAN5.EnergyMgmtBodyInfo_4 epasInfo5;

  /* CAN6 */

  message CAN6.BCM_AutoSar_Network_Mgmt bcm6;
  message CAN6.BodyInfo_3 body6;
  message CAN6.DCDCE_AutoSar_Network_Mgmt dcdce6;
  message CAN6.DCDCF_AutoSar_Network_Mgmt dcdcf6;
  message CAN6.DCDCG_AutoSar_Network_Mgmt dcdcg6;

  message CAN6.EnergyMgmtBodyCtrl_1 ebbCtrl6;
  message CAN6.EnergyMgmtBodyInfo_1 ebbInfo6;
  message CAN6.EnergyMgmtBodyCtrl_2 embCtrl6;
  message CAN6.EnergyMgmtBodyInfo_2 embInfo6;
  message CAN6.EnergyMgmtBodyCtrl_3 v48Ctrl6;
  message CAN6.EnergyMgmtBodyInfo_3 v48Info6;
  message CAN6.EnergyMgmtBodyCtrl_4 epasCtrl6;
  message CAN6.EnergyMgmtBodyInfo_4 epasInfo6;
}


/* MESSAGE INITIALIZATION */

/*
  Initialize using the same values as the
  previous configuration.

  Raw-byte values must be checked against
  your DBC before hardware transmission.
*/

#define INIT_CTRL(m) \
  m.byte(0)=30; \
  m.byte(1)=168; \
  m.byte(2)=0; \
  m.byte(3)=13; \
  m.byte(4)=52; \
  m.byte(5)=192; \
  m.byte(6)=0; \
  m.byte(7)=0;

#define INIT_INFO(m) \
  m.byte(0)=0; \
  m.byte(1)=0; \
  m.byte(2)=0; \
  m.byte(3)=0; \
  m.byte(4)=0; \
  m.byte(5)=0; \
  m.byte(6)=162; \
  m.byte(7)=128;

#define INIT_48CTRL(m) \
  m.byte(0)=254; \
  m.byte(1)=254; \
  m.byte(2)=254; \
  m.byte(3)=30; \
  m.byte(4)=0; \
  m.byte(5)=0; \
  m.byte(6)=0; \
  m.byte(7)=0;

#define INIT_48INFO(m) \
  m.byte(0)=8; \
  m.byte(1)=254; \
  m.byte(2)=254; \
  m.byte(3)=0; \
  m.byte(4)=0; \
  m.byte(5)=0; \
  m.byte(6)=0; \
  m.byte(7)=0;

#define INIT_BCM(m) \
  m.BCM_AutoSarNMNodeId=129; \
  m.BCM_AutoSarNMControl=0; \
  m.BCM_AutoSarNMReserved1=255; \
  m.BCM_AutoSarNMReserved2=255; \
  m.BCM_GWOnBoardTester=255; \
  m.BCM_GWNMProxy=255; \
  m.BCM_AutoSarNMReserved3=255; \
  m.BCM_AutoSarNMReserved4=255;

#define INIT_DCDCE(m) \
  m.DCDCE_AutoSarNMControl=0; \
  m.DCDCE_AutoSarNMNodeId=129; \
  m.DCDCE_AutoSarNMReserved1=255; \
  m.DCDCE_AutoSarNMReserved2=255; \
  m.DCDCE_GWOnBoardTester=255; \
  m.DCDCE_GWNMProxy=255; \
  m.DCDCE_AutoSarNMReserved3=255; \
  m.DCDCE_AutoSarNMReserved4=255;

#define INIT_DCDCF(m) \
  m.DCDCF_AutoSarNMControl=0; \
  m.DCDCF_AutoSarNMNodeId=129; \
  m.DCDCF_AutoSarNMReserved1=255; \
  m.DCDCF_AutoSarNMReserved2=255; \
  m.DCDCF_GWOnBoardTester=255; \
  m.DCDCF_GWNMProxy=255; \
  m.DCDCF_AutoSarNMReserved3=255; \
  m.DCDCF_AutoSarNMReserved4=255;

#define INIT_DCDCG(m) \
  m.DCDCG_AutoSarNMControl=0; \
  m.DCDCG_AutoSarNMNodeId=129; \
  m.DCDCG_AutoSarNMReserved1=255; \
  m.DCDCG_AutoSarNMReserved2=255; \
  m.DCDCG_GWOnBoardTester=255; \
  m.DCDCG_GWNMProxy=255; \
  m.DCDCG_AutoSarNMReserved3=255; \
  m.DCDCG_AutoSarNMReserved4=255;


void initMessages()
{
  /* BCM */

  INIT_BCM(bcm1)
  INIT_BCM(bcm2)
  INIT_BCM(bcm3)
  INIT_BCM(bcm4)
  INIT_BCM(bcm5)
  INIT_BCM(bcm6)

  /* DCDC NM */

  INIT_DCDCE(dcdce1)
  INIT_DCDCE(dcdce2)
  INIT_DCDCE(dcdce3)
  INIT_DCDCE(dcdce4)
  INIT_DCDCE(dcdce5)
  INIT_DCDCE(dcdce6)

  INIT_DCDCF(dcdcf1)
  INIT_DCDCF(dcdcf2)
  INIT_DCDCF(dcdcf3)
  INIT_DCDCF(dcdcf4)
  INIT_DCDCF(dcdcf5)
  INIT_DCDCF(dcdcf6)

  INIT_DCDCG(dcdcg1)
  INIT_DCDCG(dcdcg2)
  INIT_DCDCG(dcdcg3)
  INIT_DCDCG(dcdcg4)
  INIT_DCDCG(dcdcg5)
  INIT_DCDCG(dcdcg6)

  /* EBB */

  INIT_CTRL(ebbCtrl1)
  INIT_CTRL(ebbCtrl2)
  INIT_CTRL(ebbCtrl3)
  INIT_CTRL(ebbCtrl4)
  INIT_CTRL(ebbCtrl5)
  INIT_CTRL(ebbCtrl6)

  INIT_INFO(ebbInfo1)
  INIT_INFO(ebbInfo2)
  INIT_INFO(ebbInfo3)
  INIT_INFO(ebbInfo4)
  INIT_INFO(ebbInfo5)
  INIT_INFO(ebbInfo6)

  /* EMB */

  INIT_CTRL(embCtrl1)
  INIT_CTRL(embCtrl2)
  INIT_CTRL(embCtrl3)
  INIT_CTRL(embCtrl4)
  INIT_CTRL(embCtrl5)
  INIT_CTRL(embCtrl6)

  INIT_INFO(embInfo1)
  INIT_INFO(embInfo2)
  INIT_INFO(embInfo3)
  INIT_INFO(embInfo4)
  INIT_INFO(embInfo5)
  INIT_INFO(embInfo6)

  /* 48V EPAS */

  INIT_48CTRL(v48Ctrl1)
  INIT_48CTRL(v48Ctrl2)
  INIT_48CTRL(v48Ctrl3)
  INIT_48CTRL(v48Ctrl4)
  INIT_48CTRL(v48Ctrl5)
  INIT_48CTRL(v48Ctrl6)

  INIT_48INFO(v48Info1)
  INIT_48INFO(v48Info2)
  INIT_48INFO(v48Info3)
  INIT_48INFO(v48Info4)
  INIT_48INFO(v48Info5)
  INIT_48INFO(v48Info6)

  /* 12V EPAS */

  INIT_CTRL(epasCtrl1)
  INIT_CTRL(epasCtrl2)
  INIT_CTRL(epasCtrl3)
  INIT_CTRL(epasCtrl4)
  INIT_CTRL(epasCtrl5)
  INIT_CTRL(epasCtrl6)

  INIT_INFO(epasInfo1)
  INIT_INFO(epasInfo2)
  INIT_INFO(epasInfo3)
  INIT_INFO(epasInfo4)
  INIT_INFO(epasInfo5)
  INIT_INFO(epasInfo6)

  /* BodyInfo_3 */

  if(sys1!=0)
  {
    body1.Parklamp_Status=1;
    body1.Ignition_Status=4;
  }

  if(sys2!=0)
  {
    body2.Parklamp_Status=1;
    body2.Ignition_Status=4;
  }

  if(sys3!=0)
  {
    body3.Parklamp_Status=1;
    body3.Ignition_Status=4;
  }

  if(sys4!=0)
  {
    body4.Parklamp_Status=1;
    body4.Ignition_Status=4;
  }

  if(sys5!=0)
  {
    body5.Parklamp_Status=1;
    body5.Ignition_Status=4;
  }

  if(sys6!=0)
  {
    body6.Parklamp_Status=1;
    body6.Ignition_Status=4;
  }
}


/* MODE CONTROL */

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

  if(sys3==1) ebbCtrl3.EMduleMde_D_Rq=mode;
  else if(sys3==2) embCtrl3.EMduleMde_D_Rq2=mode;
  else if(sys3==3) v48Ctrl3.UCapMduleMde_D_Rq=mode;
  else if(sys3==4) epasCtrl3.EMduleMde_D_Rq3=mode;

  if(sys4==1) ebbCtrl4.EMduleMde_D_Rq=mode;
  else if(sys4==2) embCtrl4.EMduleMde_D_Rq2=mode;
  else if(sys4==3) v48Ctrl4.UCapMduleMde_D_Rq=mode;
  else if(sys4==4) epasCtrl4.EMduleMde_D_Rq3=mode;

  if(sys5==1) ebbCtrl5.EMduleMde_D_Rq=mode;
  else if(sys5==2) embCtrl5.EMduleMde_D_Rq2=mode;
  else if(sys5==3) v48Ctrl5.UCapMduleMde_D_Rq=mode;
  else if(sys5==4) epasCtrl5.EMduleMde_D_Rq3=mode;

  if(sys6==1) ebbCtrl6.EMduleMde_D_Rq=mode;
  else if(sys6==2) embCtrl6.EMduleMde_D_Rq2=mode;
  else if(sys6==3) v48Ctrl6.UCapMduleMde_D_Rq=mode;
  else if(sys6==4) epasCtrl6.EMduleMde_D_Rq3=mode;
}


/* ISOLATION CONTROL
   0 = OPEN
   1 = CLOSE
   SKIP 48V EPAS
*/

void setIsolation(int value)
{
  if(sys1==1) ebbCtrl1.IsolSwtch_B_Cmd=value;
  else if(sys1==2) embCtrl1.IsolSwtch_B_Cmd2=value;
  else if(sys1==4) epasCtrl1.IsolSwtch_B_Cmd3=value;

  if(sys2==1) ebbCtrl2.IsolSwtch_B_Cmd=value;
  else if(sys2==2) embCtrl2.IsolSwtch_B_Cmd2=value;
  else if(sys2==4) epasCtrl2.IsolSwtch_B_Cmd3=value;

  if(sys3==1) ebbCtrl3.IsolSwtch_B_Cmd=value;
  else if(sys3==2) embCtrl3.IsolSwtch_B_Cmd2=value;
  else if(sys3==4) epasCtrl3.IsolSwtch_B_Cmd3=value;

  if(sys4==1) ebbCtrl4.IsolSwtch_B_Cmd=value;
  else if(sys4==2) embCtrl4.IsolSwtch_B_Cmd2=value;
  else if(sys4==4) epasCtrl4.IsolSwtch_B_Cmd3=value;

  if(sys5==1) ebbCtrl5.IsolSwtch_B_Cmd=value;
  else if(sys5==2) embCtrl5.IsolSwtch_B_Cmd2=value;
  else if(sys5==4) epasCtrl5.IsolSwtch_B_Cmd3=value;

  if(sys6==1) ebbCtrl6.IsolSwtch_B_Cmd=value;
  else if(sys6==2) embCtrl6.IsolSwtch_B_Cmd2=value;
  else if(sys6==4) epasCtrl6.IsolSwtch_B_Cmd3=value;
}


/* TRANSMIT CONTROL + INFO EVERY 100 MS */

void send100()
{
  if(sys1==1) { output(ebbCtrl1); output(ebbInfo1); }
  else if(sys1==2) { output(embCtrl1); output(embInfo1); }
  else if(sys1==3) { output(v48Ctrl1); output(v48Info1); }
  else if(sys1==4) { output(epasCtrl1); output(epasInfo1); }

  if(sys2==1) { output(ebbCtrl2); output(ebbInfo2); }
  else if(sys2==2) { output(embCtrl2); output(embInfo2); }
  else if(sys2==3) { output(v48Ctrl2); output(v48Info2); }
  else if(sys2==4) { output(epasCtrl2); output(epasInfo2); }

  if(sys3==1) { output(ebbCtrl3); output(ebbInfo3); }
  else if(sys3==2) { output(embCtrl3); output(embInfo3); }
  else if(sys3==3) { output(v48Ctrl3); output(v48Info3); }
  else if(sys3==4) { output(epasCtrl3); output(epasInfo3); }

  if(sys4==1) { output(ebbCtrl4); output(ebbInfo4); }
  else if(sys4==2) { output(embCtrl4); output(embInfo4); }
  else if(sys4==3) { output(v48Ctrl4); output(v48Info4); }
  else if(sys4==4) { output(epasCtrl4); output(epasInfo4); }

  if(sys5==1) { output(ebbCtrl5); output(ebbInfo5); }
  else if(sys5==2) { output(embCtrl5); output(embInfo5); }
  else if(sys5==3) { output(v48Ctrl5); output(v48Info5); }
  else if(sys5==4) { output(epasCtrl5); output(epasInfo5); }

  if(sys6==1) { output(ebbCtrl6); output(ebbInfo6); }
  else if(sys6==2) { output(embCtrl6); output(embInfo6); }
  else if(sys6==3) { output(v48Ctrl6); output(v48Info6); }
  else if(sys6==4) { output(epasCtrl6); output(epasInfo6); }
}


/* BODY INFO EVERY 500 MS */

void send500()
{
  if(sys1!=0) output(body1);
  if(sys2!=0) output(body2);
  if(sys3!=0) output(body3);
  if(sys4!=0) output(body4);
  if(sys5!=0) output(body5);
  if(sys6!=0) output(body6);
}


/* NETWORK MANAGEMENT EVERY 1000 MS */

void send1000()
{
  if(sys1!=0) output(bcm1);
  if(sys2!=0) output(bcm2);
  if(sys3!=0) output(bcm3);
  if(sys4!=0) output(bcm4);
  if(sys5!=0) output(bcm5);
  if(sys6!=0) output(bcm6);

  /* EBB */

  if(sys1==1) { output(dcdcf1); output(dcdcg1); }
  if(sys2==1) { output(dcdcf2); output(dcdcg2); }
  if(sys3==1) { output(dcdcf3); output(dcdcg3); }
  if(sys4==1) { output(dcdcf4); output(dcdcg4); }
  if(sys5==1) { output(dcdcf5); output(dcdcg5); }
  if(sys6==1) { output(dcdcf6); output(dcdcg6); }

  /* EMB */

  if(sys1==2) { output(dcdce1); output(dcdcf1); }
  if(sys2==2) { output(dcdce2); output(dcdcf2); }
  if(sys3==2) { output(dcdce3); output(dcdcf3); }
  if(sys4==2) { output(dcdce4); output(dcdcf4); }
  if(sys5==2) { output(dcdce5); output(dcdcf5); }
  if(sys6==2) { output(dcdce6); output(dcdcf6); }

  /* 48V EPAS */

  if(sys1==3) { output(dcdce1); output(dcdcg1); }
  if(sys2==3) { output(dcdce2); output(dcdcg2); }
  if(sys3==3) { output(dcdce3); output(dcdcg3); }
  if(sys4==3) { output(dcdce4); output(dcdcg4); }
  if(sys5==3) { output(dcdce5); output(dcdcg5); }
  if(sys6==3) { output(dcdce6); output(dcdcg6); }

  /* 12V EPAS */

  if(sys1==4) output(dcdcg1);
  if(sys2==4) output(dcdcg2);
  if(sys3==4) output(dcdcg3);
  if(sys4==4) output(dcdcg4);
  if(sys5==4) output(dcdcg5);
  if(sys6==4) output(dcdcg6);
}


/* STOP TEST */

void stopTest()
{
  /* Command OFF and isolation CLOSE */

  setMode(0);
  setIsolation(1);

  send100();

  cancelTimer(t100);
  cancelTimer(t500);
  cancelTimer(t1000);
  cancelTimer(seqTimer);

  testRunning=0;
  step=0;

  write("TEST STOPPED - OFF COMMANDED");
}


/* MEASUREMENT START */

on start
{
  sys1=0;
  sys2=0;
  sys3=0;
  sys4=0;
  sys5=0;
  sys6=0;

  testRunning=0;
  step=0;
  cycle=0;

  @sysvar::MasterCtrl::StartTest=0;
  @sysvar::MasterCtrl::StopTest=0;

  write("======================================");
  write("CANALYZER MEASUREMENT STARTED");
  write("WAITING FOR PANEL START TEST");
  write("======================================");
}


/* PANEL START BUTTON */

on sysvar MasterCtrl::StartTest
{
  int active;

  if(@this==1 && testRunning==0)
  {
    sys1=@sysvar::CH1::Module;
    sys2=@sysvar::CH2::Module;
    sys3=@sysvar::CH3::Module;
    sys4=@sysvar::CH4::Module;
    sys5=@sysvar::CH5::Module;
    sys6=@sysvar::CH6::Module;

    active=0;

    if(sys1!=0) active++;
    if(sys2!=0) active++;
    if(sys3!=0) active++;
    if(sys4!=0) active++;
    if(sys5!=0) active++;
    if(sys6!=0) active++;

    if(active==0)
    {
      write("NO SYSTEM SELECTED");
      @sysvar::MasterCtrl::StartTest=0;
      return;
    }

    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);

    testRunning=1;
    step=0;
    cycle=0;

    initMessages();

    setMode(0);
    setIsolation(1);

    send100();
    send500();
    send1000();

    setTimer(t100,100);
    setTimer(t500,500);
    setTimer(t1000,1000);

    write("======================================");
    write("HUMIDITY TEST STARTED");
    write("INITIAL OFF - 2 SECONDS");
    write("======================================");

    write("CAN1=%d CAN2=%d CAN3=%d",
          sys1,sys2,sys3);

    write("CAN4=%d CAN5=%d CAN6=%d",
          sys4,sys5,sys6);

    setTimer(seqTimer,2000);
  }

  if(@this==1)
    @sysvar::MasterCtrl::StartTest=0;
}


/* PANEL STOP BUTTON */

on sysvar MasterCtrl::StopTest
{
  if(@this==1)
  {
    if(testRunning)
    {
      stopTest();
    }

    @sysvar::MasterCtrl::StopTest=0;
  }
}


/* PERIODIC TIMERS */

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
    send1000();
    setTimer(t1000,1000);
  }
}


/* HUMIDITY TEST - 2 CYCLES */

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

  /* CYCLE 1 - FLOAT */

  else if(step==1)
  {
    cycle=1;

    setMode(3);
    setIsolation(0);

    write("CYCLE 1 - FLOAT");
    write("ISOLATION OPEN - 1 SEC");

    step=2;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 1 - ISOLATION CLOSE */

  else if(step==2)
  {
    setIsolation(1);

    write("CYCLE 1 - ISOLATION CLOSE");
    write("FLOAT CONTINUES - 4 SEC");

    step=3;
    setTimer(seqTimer,4000);
  }

  /* CYCLE 1 - STANDBY */

  else if(step==3)
  {
    setMode(1);
    setIsolation(1);

    write("CYCLE 1 COMPLETE");
    write("STANDBY - 2 SEC");

    step=4;
    setTimer(seqTimer,2000);
  }

  /* CYCLE 2 - FLOAT */

  else if(step==4)
  {
    cycle=2;

    setMode(3);
    setIsolation(0);

    write("CYCLE 2 - FLOAT");
    write("ISOLATION OPEN - 1 SEC");

    step=5;
    setTimer(seqTimer,1000);
  }

  /* CYCLE 2 - ISOLATION CLOSE */

  else if(step==5)
  {
    setIsolation(1);

    write("CYCLE 2 - ISOLATION CLOSE");
    write("FLOAT CONTINUES - 4 SEC");

    step=6;
    setTimer(seqTimer,4000);
  }

  /* CYCLE 2 - STANDBY */

  else if(step==6)
  {
    setMode(1);
    setIsolation(1);

    write("CYCLE 2 COMPLETE");
    write("STANDBY - 2 SEC");

    step=7;
    setTimer(seqTimer,2000);
  }

  /* FINISH */

  else if(step==7)
  {
    stopTest();

    write("======================================");
    write("2 CYCLE HUMIDITY TEST COMPLETE");
    write("FINAL MODE - OFF COMMANDED");
    write("======================================");
  }
}
