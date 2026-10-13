


/*@!Encoding:1252*/

variables
{
  /* 0=NONE, 1=EBB, 2=EMB,
     3=48V EPAS, 4=12V EPAS */

  int sys1=4; // CAN1 EPAS
  int sys2=1; // CAN2 EBB

  msTimer t100,t500,t1000,seqTimer;
  int step=0;

  /* CAN1 - BCM6_BCM_CANFD */

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

  /* CAN2 - CANdb1 */

  message CANdb1::BCM_AutoSar_Network_Mgmt bcm2;
  message CANdb1::BodyInfo_3 body2;
  message CANdb1::DCDCE_AutoSar_Network_Mgmt dcdce2;
  message CANdb1::DCDCF_AutoSar_Network_Mgmt dcdcf2;
  message CANdb1::DCDCG_AutoSar_Network_Mgmt dcdcg2;

  message CANdb1::EnergyMgmtBodyCtrl_1 ebbCtrl2;
  message CANdb1::EnergyMgmtBodyInfo_1 ebbInfo2;
  message CANdb1::EnergyMgmtBodyCtrl_2 embCtrl2;
  message CANdb1::EnergyMgmtBodyInfo_2 embInfo2;
  message CANdb1::EnergyMgmtBodyCtrl_3 v48Ctrl2;
  message CANdb1::EnergyMgmtBodyInfo_3 v48Info2;
  message CANdb1::EnergyMgmtBodyCtrl_4 epasCtrl2;
  message CANdb1::EnergyMgmtBodyInfo_4 epasInfo2;
}

void initMessages()
{
  /* BCM CAN1 */

  bcm1.BCM_AutoSarNMNodeId=129;
  bcm1.BCM_AutoSarNMControl=0;
  bcm1.BCM_AutoSarNMReserved1=255;
  bcm1.BCM_AutoSarNMReserved2=255;
  bcm1.BCM_GWOnBoardTester=255;
  bcm1.BCM_GWNMProxy=255;
  bcm1.BCM_AutoSarNMReserved3=255;
  bcm1.BCM_AutoSarNMReserved4=255;

  /* BCM CAN2 */

  bcm2.BCM_AutoSarNMNodeId=129;
  bcm2.BCM_AutoSarNMControl=0;
  bcm2.BCM_AutoSarNMReserved1=255;
  bcm2.BCM_AutoSarNMReserved2=255;
  bcm2.BCM_GWOnBoardTester=255;
  bcm2.BCM_GWNMProxy=255;
  bcm2.BCM_AutoSarNMReserved3=255;
  bcm2.BCM_AutoSarNMReserved4=255;

  /* NM CAN1 */

  dcdce1.byte(0)=0;
  dcdce1.byte(1)=129;
  dcdce1.byte(2)=255;
  dcdce1.byte(3)=255;
  dcdce1.byte(4)=255;
  dcdce1.byte(5)=255;
  dcdce1.byte(6)=255;
  dcdce1.byte(7)=255;

  dcdcf1.byte(0)=0;
  dcdcf1.byte(1)=129;
  dcdcf1.byte(2)=255;
  dcdcf1.byte(3)=255;
  dcdcf1.byte(4)=255;
  dcdcf1.byte(5)=255;
  dcdcf1.byte(6)=255;
  dcdcf1.byte(7)=255;

  dcdcg1.byte(0)=0;
  dcdcg1.byte(1)=129;
  dcdcg1.byte(2)=255;
  dcdcg1.byte(3)=255;
  dcdcg1.byte(4)=255;
  dcdcg1.byte(5)=255;
  dcdcg1.byte(6)=255;
  dcdcg1.byte(7)=255;

  /* NM CAN2 */

  dcdce2.byte(0)=0;
  dcdce2.byte(1)=129;
  dcdce2.byte(2)=255;
  dcdce2.byte(3)=255;
  dcdce2.byte(4)=255;
  dcdce2.byte(5)=255;
  dcdce2.byte(6)=255;
  dcdce2.byte(7)=255;

  dcdcf2.byte(0)=0;
  dcdcf2.byte(1)=129;
  dcdcf2.byte(2)=255;
  dcdcf2.byte(3)=255;
  dcdcf2.byte(4)=255;
  dcdcf2.byte(5)=255;
  dcdcf2.byte(6)=255;
  dcdcf2.byte(7)=255;

  dcdcg2.byte(0)=0;
  dcdcg2.byte(1)=129;
  dcdcg2.byte(2)=255;
  dcdcg2.byte(3)=255;
  dcdcg2.byte(4)=255;
  dcdcg2.byte(5)=255;
  dcdcg2.byte(6)=255;
  dcdcg2.byte(7)=255;

  /* CONTROL CAN1 */

  ebbCtrl1.byte(0)=30;
  ebbCtrl1.byte(1)=168;
  ebbCtrl1.byte(2)=0;
  ebbCtrl1.byte(3)=13;
  ebbCtrl1.byte(4)=52;
  ebbCtrl1.byte(5)=192;
  ebbCtrl1.byte(6)=0;
  ebbCtrl1.byte(7)=0;

  embCtrl1.byte(0)=30;
  embCtrl1.byte(1)=168;
  embCtrl1.byte(2)=0;
  embCtrl1.byte(3)=13;
  embCtrl1.byte(4)=52;
  embCtrl1.byte(5)=192;
  embCtrl1.byte(6)=0;
  embCtrl1.byte(7)=0;

  epasCtrl1.byte(0)=30;
  epasCtrl1.byte(1)=168;
  epasCtrl1.byte(2)=0;
  epasCtrl1.byte(3)=13;
  epasCtrl1.byte(4)=52;
  epasCtrl1.byte(5)=192;
  epasCtrl1.byte(6)=0;
  epasCtrl1.byte(7)=0;

  v48Ctrl1.byte(0)=254;
  v48Ctrl1.byte(1)=254;
  v48Ctrl1.byte(2)=254;
  v48Ctrl1.byte(3)=30;
  v48Ctrl1.byte(4)=0;
  v48Ctrl1.byte(5)=0;
  v48Ctrl1.byte(6)=0;
  v48Ctrl1.byte(7)=0;

  /* CONTROL CAN2 */

  ebbCtrl2.byte(0)=30;
  ebbCtrl2.byte(1)=168;
  ebbCtrl2.byte(2)=0;
  ebbCtrl2.byte(3)=13;
  ebbCtrl2.byte(4)=52;
  ebbCtrl2.byte(5)=192;
  ebbCtrl2.byte(6)=0;
  ebbCtrl2.byte(7)=0;

  embCtrl2.byte(0)=30;
  embCtrl2.byte(1)=168;
  embCtrl2.byte(2)=0;
  embCtrl2.byte(3)=13;
  embCtrl2.byte(4)=52;
  embCtrl2.byte(5)=192;
  embCtrl2.byte(6)=0;
  embCtrl2.byte(7)=0;

  epasCtrl2.byte(0)=30;
  epasCtrl2.byte(1)=168;
  epasCtrl2.byte(2)=0;
  epasCtrl2.byte(3)=13;
  epasCtrl2.byte(4)=52;
  epasCtrl2.byte(5)=192;
  epasCtrl2.byte(6)=0;
  epasCtrl2.byte(7)=0;

  v48Ctrl2.byte(0)=254;
  v48Ctrl2.byte(1)=254;
  v48Ctrl2.byte(2)=254;
  v48Ctrl2.byte(3)=30;
  v48Ctrl2.byte(4)=0;
  v48Ctrl2.byte(5)=0;
  v48Ctrl2.byte(6)=0;
  v48Ctrl2.byte(7)=0;

  /* INFO CAN1 */

  ebbInfo1.byte(0)=0;
  ebbInfo1.byte(1)=0;
  ebbInfo1.byte(2)=0;
  ebbInfo1.byte(3)=0;
  ebbInfo1.byte(4)=0;
  ebbInfo1.byte(5)=0;
  ebbInfo1.byte(6)=162;
  ebbInfo1.byte(7)=128;

  embInfo1.byte(0)=0;
  embInfo1.byte(1)=0;
  embInfo1.byte(2)=0;
  embInfo1.byte(3)=0;
  embInfo1.byte(4)=0;
  embInfo1.byte(5)=0;
  embInfo1.byte(6)=162;
  embInfo1.byte(7)=128;

  epasInfo1.byte(0)=0;
  epasInfo1.byte(1)=0;
  epasInfo1.byte(2)=0;
  epasInfo1.byte(3)=0;
  epasInfo1.byte(4)=0;
  epasInfo1.byte(5)=0;
  epasInfo1.byte(6)=162;
  epasInfo1.byte(7)=128;

  v48Info1.byte(0)=8;
  v48Info1.byte(1)=254;
  v48Info1.byte(2)=254;
  v48Info1.byte(3)=0;
  v48Info1.byte(4)=0;
  v48Info1.byte(5)=0;
  v48Info1.byte(6)=0;
  v48Info1.byte(7)=0;

  /* INFO CAN2 */

  ebbInfo2.byte(0)=0;
  ebbInfo2.byte(1)=0;
  ebbInfo2.byte(2)=0;
  ebbInfo2.byte(3)=0;
  ebbInfo2.byte(4)=0;
  ebbInfo2.byte(5)=0;
  ebbInfo2.byte(6)=162;
  ebbInfo2.byte(7)=128;

  embInfo2.byte(0)=0;
  embInfo2.byte(1)=0;
  embInfo2.byte(2)=0;
  embInfo2.byte(3)=0;
  embInfo2.byte(4)=0;
  embInfo2.byte(5)=0;
  embInfo2.byte(6)=162;
  embInfo2.byte(7)=128;

  epasInfo2.byte(0)=0;
  epasInfo2.byte(1)=0;
  epasInfo2.byte(2)=0;
  epasInfo2.byte(3)=0;
  epasInfo2.byte(4)=0;
  epasInfo2.byte(5)=0;
  epasInfo2.byte(6)=162;
  epasInfo2.byte(7)=128;

  v48Info2.byte(0)=8;
  v48Info2.byte(1)=254;
  v48Info2.byte(2)=254;
  v48Info2.byte(3)=0;
  v48Info2.byte(4)=0;
  v48Info2.byte(5)=0;
  v48Info2.byte(6)=0;
  v48Info2.byte(7)=0;

  /* IGNITION RUN, PARKLAMP ON */

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
}

/* MODE: OFF=0, STANDBY=1, FLOAT=3 */

void setMode(int value)
{
  if(sys1==1)
    ebbCtrl1.EMduleMde_D_Rq=value;
  else if(sys1==2)
    embCtrl1.EMduleMde_D_Rq2=value;
  else if(sys1==3)
    v48Ctrl1.UCapMduleMde_D_Rq=value;
  else if(sys1==4)
    epasCtrl1.EMduleMde_D_Rq3=value;

  if(sys2==1)
    ebbCtrl2.EMduleMde_D_Rq=value;
  else if(sys2==2)
    embCtrl2.EMduleMde_D_Rq2=value;
  else if(sys2==3)
    v48Ctrl2.UCapMduleMde_D_Rq=value;
  else if(sys2==4)
    epasCtrl2.EMduleMde_D_Rq3=value;
}

/* ISOLATION: OPEN=0, CLOSE=1 */

void setIsolation(int value)
{
  if(sys1==1)
    ebbCtrl1.IsolSwtch_B_Cmd=value;
  else if(sys1==2)
    embCtrl1.IsolSwtch_B_Cmd2=value;
  else if(sys1==4)
    epasCtrl1.IsolSwtch_B_Cmd3=value;

  if(sys2==1)
    ebbCtrl2.IsolSwtch_B_Cmd=value;
  else if(sys2==2)
    embCtrl2.IsolSwtch_B_Cmd2=value;
  else if(sys2==4)
    epasCtrl2.IsolSwtch_B_Cmd3=value;
}

/* TRANSMIT CONTROL + INFO EVERY 100 MS */

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
  if(sys1!=0)
    output(body1);

  if(sys2!=0)
    output(body2);
}

/* NETWORK MANAGEMENT EVERY 1000 MS */

void send1000()
{
  if(sys1!=0)
    output(bcm1);

  if(sys2!=0)
    output(bcm2);

  /* CAN1 EBB */
  if(sys1==1)
  {
    output(dcdcf1);
    output(dcdcg1);
  }

  /* CAN1 EMB */
  if(sys1==2)
  {
    output(dcdce1);
    output(dcdcf1);
  }

  /* CAN1 48V EPAS */
  if(sys1==3)
  {
    output(dcdce1);
    output(dcdcg1);
  }

  /* CAN1 12V EPAS */
  if(sys1==4)
    output(dcdcg1);

  /* CAN2 EBB */
  if(sys2==1)
  {
    output(dcdcf2);
    output(dcdcg2);
  }

  /* CAN2 EMB */
  if(sys2==2)
  {
    output(dcdce2);
    output(dcdcf2);
  }

  /* CAN2 48V EPAS */
  if(sys2==3)
  {
    output(dcdce2);
    output(dcdcg2);
  }

  /* CAN2 12V EPAS */
  if(sys2==4)
    output(dcdcg2);
}

/* START MEASUREMENT */

on start
{
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

  write("START - OFF 2 SEC");

  setTimer(seqTimer,2000);
}

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

/* TWO-MINUTE TEST
   OFF: 2 SECONDS
   STANDBY: 2 SECONDS
   FLOAT: 120 SECONDS TOTAL
   ISOLATION OPEN: FIRST 1 SECOND
   ISOLATION CLOSE: REMAINING 119 SEC
   STANDBY: 6 SECONDS
   STOP MEASUREMENT
*/

on timer seqTimer
{
  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("STANDBY - 2 SEC");

    step=1;
    setTimer(seqTimer,2000);
  }

  else if(step==1)
  {
    setMode(3);
    setIsolation(0);

    write("FLOAT - ISOLATION OPEN - 1 SEC");

    step=2;
    setTimer(seqTimer,1000);
  }

  else if(step==2)
  {
    setIsolation(1);

    write("ISOLATION CLOSE - FLOAT 119 SEC");

    step=3;
    setTimer(seqTimer,119000);
  }

  else if(step==3)
  {
    setMode(1);
    setIsolation(1);

    write("FLOAT COMPLETE - STANDBY 6 SEC");

    step=4;
    setTimer(seqTimer,6000);
  }

  else if(step==4)
  {
    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);

    write("2 MIN TEST COMPLETE - MEASUREMENT STOP");

    stop();
  }
}
