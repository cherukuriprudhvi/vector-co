


/*@!Encoding:1252*/
variables
{
  /* SYSTEM SELECTION:
     0 = NONE
     1 = EBB
     2 = EMB
     3 = 48V EPAS
     4 = 12V EPAS
  */

  int sys1 = 4;

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seqTimer;

  int step = 0;

  /* CAN1 - ONE SELECTED SYSTEM */

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
  /* BCM NETWORK MANAGEMENT */

  bcm1.BCM_AutoSarNMNodeId = 129;
  bcm1.BCM_AutoSarNMControl = 0;
  bcm1.BCM_AutoSarNMReserved1 = 255;
  bcm1.BCM_AutoSarNMReserved2 = 255;
  bcm1.BCM_GWOnBoardTester = 255;
  bcm1.BCM_GWNMProxy = 255;
  bcm1.BCM_AutoSarNMReserved3 = 255;
  bcm1.BCM_AutoSarNMReserved4 = 255;

  /* DCDCE NETWORK MANAGEMENT */

  dcdce1.DCDCE_AutoSarNMControl = 0;
  dcdce1.DCDCE_AutoSarNMNodeId = 129;
  dcdce1.DCDCE_AutoSarNMReserved1 = 255;
  dcdce1.DCDCE_AutoSarNMReserved2 = 255;
  dcdce1.DCDCE_GWOnBoardTester = 255;
  dcdce1.DCDCE_GWNMProxy = 255;
  dcdce1.DCDCE_AutoSarNMReserved3 = 255;
  dcdce1.DCDCE_AutoSarNMReserved4 = 255;

  /* DCDCF NETWORK MANAGEMENT */

  dcdcf1.DCDCF_AutoSarNMControl = 0;
  dcdcf1.DCDCF_AutoSarNMNodeId = 129;
  dcdcf1.DCDCF_AutoSarNMReserved1 = 255;
  dcdcf1.DCDCF_AutoSarNMReserved2 = 255;
  dcdcf1.DCDCF_GWOnBoardTester = 255;
  dcdcf1.DCDCF_GWNMProxy = 255;
  dcdcf1.DCDCF_AutoSarNMReserved3 = 255;
  dcdcf1.DCDCF_AutoSarNMReserved4 = 255;

  /* DCDCG NETWORK MANAGEMENT */

  dcdcg1.DCDCG_AutoSarNMControl = 0;
  dcdcg1.DCDCG_AutoSarNMNodeId = 129;
  dcdcg1.DCDCG_AutoSarNMReserved1 = 255;
  dcdcg1.DCDCG_AutoSarNMReserved2 = 255;
  dcdcg1.DCDCG_GWOnBoardTester = 255;
  dcdcg1.DCDCG_GWNMProxy = 255;
  dcdcg1.DCDCG_AutoSarNMReserved3 = 255;
  dcdcg1.DCDCG_AutoSarNMReserved4 = 255;

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

  ebbInfo1.byte(0)=0;
  ebbInfo1.byte(1)=0;
  ebbInfo1.byte(2)=0;
  ebbInfo1.byte(3)=0;
  ebbInfo1.byte(4)=0;
  ebbInfo1.byte(5)=0;
  ebbInfo1.byte(6)=162;
  ebbInfo1.byte(7)=128;

  /* EMB INFORMATION */

  embInfo1.byte(0)=0;
  embInfo1.byte(1)=0;
  embInfo1.byte(2)=0;
  embInfo1.byte(3)=0;
  embInfo1.byte(4)=0;
  embInfo1.byte(5)=0;
  embInfo1.byte(6)=162;
  embInfo1.byte(7)=128;

  /* 12V EPAS INFORMATION */

  epasInfo1.byte(0)=0;
  epasInfo1.byte(1)=0;
  epasInfo1.byte(2)=0;
  epasInfo1.byte(3)=0;
  epasInfo1.byte(4)=0;
  epasInfo1.byte(5)=0;
  epasInfo1.byte(6)=162;
  epasInfo1.byte(7)=128;

  /* 48V EPAS INFORMATION
     IMPORTANT: BYTE 0 MUST REMAIN 8 */

  v48Info1.byte(0)=8;
  v48Info1.byte(1)=254;
  v48Info1.byte(2)=254;
  v48Info1.byte(3)=0;
  v48Info1.byte(4)=0;
  v48Info1.byte(5)=0;
  v48Info1.byte(6)=0;
  v48Info1.byte(7)=0;

  /* BODY INFO - ALL ACTIVE SYSTEMS */

  if(sys1!=0)
  {
    body1.Parklamp_Status=1;
    body1.Ignition_Status=4;
  }
}


/* MODE:
   0 = OFF
   1 = STANDBY
   3 = FLOAT
*/

void setMode(int mode)
{
  if(sys1==1)
    ebbCtrl1.EMduleMde_D_Rq=mode;

  else if(sys1==2)
    embCtrl1.EMduleMde_D_Rq2=mode;

  else if(sys1==3)
    v48Ctrl1.UCapMduleMde_D_Rq=mode;

  else if(sys1==4)
    epasCtrl1.EMduleMde_D_Rq3=mode;
}


/* ISOLATION:
   0 = OPEN
   1 = CLOSE
   48V EPAS HAS NO ISOLATION COMMAND
*/

void setIsolation(int value)
{
  if(sys1==1)
    ebbCtrl1.IsolSwtch_B_Cmd=value;

  else if(sys1==2)
    embCtrl1.IsolSwtch_B_Cmd2=value;

  else if(sys1==4)
    epasCtrl1.IsolSwtch_B_Cmd3=value;
}


/* TRANSMIT EVERY 100 MS */

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


/* TRANSMIT BODY INFO EVERY 500 MS */

void send500()
{
  if(sys1!=0)
    output(body1);
}


/* TRANSMIT NETWORK MANAGEMENT EVERY 1000 MS */

void send1000()
{
  if(sys1!=0)
    output(bcm1);

  /* EBB */

  if(sys1==1)
  {
    output(dcdcf1);
    output(dcdcg1);
  }

  /* EMB */

  if(sys1==2)
  {
    output(dcdce1);
    output(dcdcf1);
  }

  /* 48V EPAS */

  if(sys1==3)
  {
    output(dcdce1);
    output(dcdcg1);
  }

  /* 12V EPAS */

  if(sys1==4)
  {
    output(dcdcg1);
  }
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

  write("OFF - 1 SEC");

  setTimer(seqTimer,1000);
}


/* PERIODIC TRANSMISSION */

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

    write("STANDBY - 1 SEC");

    step=1;
    setTimer(seqTimer,1000);
  }

  else if(step==1)
  {
    setMode(3);
    setIsolation(1);

    write("FLOAT - 1 SEC");

    step=2;
    setTimer(seqTimer,1000);
  }

  else if(step==2)
  {
    setIsolation(0);

    write("ISOLATION OPEN - 1 SEC");

    step=3;
    setTimer(seqTimer,1000);
  }

  else if(step==3)
  {
    setIsolation(1);

    write("ISOLATION CLOSE - 1 SEC");

    step=4;
    setTimer(seqTimer,1000);
  }

  else if(step==4)
  {
    write("FLOAT - 2 MIN");

    step=5;
    setTimer(seqTimer,120000);
  }

  else if(step==5)
  {
    setMode(1);
    setIsolation(1);

    write("STANDBY - 1 SEC");

    step=6;
    setTimer(seqTimer,1000);
  }

  else if(step==6)
  {
    setMode(0);
    setIsolation(1);

    send100();

    write("OFF - 1 SEC");

    step=7;
    setTimer(seqTimer,1000);
  }

  else if(step==7)
  {
    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);

    write("TEST COMPLETE");

    stop();
  }
}
