

variables
{
  message DBC5::BCM_AutoSar_Network_Mgmt       bcm;
  message DBC5::BodyInfo_3                     body;
  message DBC5::DCDCE_AutoSar_Network_Mgmt     dcdce;
  message DBC5::DCDCG_AutoSar_Network_Mgmt     dcdcg;
  message DBC5::EnergyMgmtBodyCtrl_3            ctrl;
  message DBC5::EnergyMgmtBodyInfo_3            info;

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seq;

  int step = 0;
}


void init48V()
{
  /* BCM: 129 0 255 255 255 255 255 255 */
  bcm.byte(0)=129;
  bcm.byte(1)=0;
  bcm.byte(2)=255;
  bcm.byte(3)=255;
  bcm.byte(4)=255;
  bcm.byte(5)=255;
  bcm.byte(6)=255;
  bcm.byte(7)=255;


  /* BODY INFO
     Working IG base:
     04 00 00 0C E6 ...
     IMPORTANT: Ignition_Status = 4 / RUN
     Set through signal so correct packed bits are used.
  */

  body.byte(0)=4;
  body.byte(1)=0;
  body.byte(2)=0;
  body.byte(3)=12;
  body.byte(4)=230;
  body.byte(5)=0;
  body.byte(6)=0;
  body.byte(7)=0;

  body.Ignition_Status = 4;


  /* DCDCE */
  dcdce.byte(0)=0;
  dcdce.byte(1)=129;
  dcdce.byte(2)=255;
  dcdce.byte(3)=255;
  dcdce.byte(4)=255;
  dcdce.byte(5)=255;
  dcdce.byte(6)=255;
  dcdce.byte(7)=255;


  /* DCDCG */
  dcdcg.byte(0)=0;
  dcdcg.byte(1)=129;
  dcdcg.byte(2)=255;
  dcdcg.byte(3)=255;
  dcdcg.byte(4)=255;
  dcdcg.byte(5)=255;
  dcdcg.byte(6)=255;
  dcdcg.byte(7)=255;


  /* 48V CONTROL 0x212
     Working captured defaults:
     FE FE FE 1E 00 00 00 00
  */

  ctrl.byte(0)=254;
  ctrl.byte(1)=254;
  ctrl.byte(2)=254;
  ctrl.byte(3)=30;
  ctrl.byte(4)=0;
  ctrl.byte(5)=0;
  ctrl.byte(6)=0;
  ctrl.byte(7)=0;

  ctrl.UCapMduleMde_D_Rq = 0;


  /* 48V INFO 0x202
     IMPORTANT:
     Aux current raw = 8 = physical 4.0
     Charge/Discharge = 254
  */

  info.byte(0)=8;
  info.byte(1)=254;
  info.byte(2)=254;
  info.byte(3)=0;
  info.byte(4)=0;
  info.byte(5)=0;
  info.byte(6)=0;
  info.byte(7)=0;
}


on start
{
  init48V();

  ctrl.UCapMduleMde_D_Rq = 0;   // OFF

  step = 0;

  setTimer(t100,100);
  setTimer(t500,500);
  setTimer(t1000,1000);

  setTimer(seq,1000);

  write("48V -> OFF");
}


/* CTRL + INFO = 100 ms */

on timer t100
{
  output(ctrl);
  output(info);

  setTimer(t100,100);
}


/* BODY = 500 ms */

on timer t500
{
  output(body);

  setTimer(t500,500);
}


/* NETWORK MANAGEMENT = 1000 ms */

on timer t1000
{
  output(bcm);
  output(dcdce);
  output(dcdcg);

  setTimer(t1000,1000);
}


/* TEST SEQUENCE */

on timer seq
{
  switch(step)
  {
    case 0:

      ctrl.UCapMduleMde_D_Rq = 1;   // STANDBY

      write("48V -> STANDBY");

      step = 1;
      setTimer(seq,1000);
      break;


    case 1:

      ctrl.UCapMduleMde_D_Rq = 3;   // FLOAT

      write("48V -> FLOAT 10 SEC");

      step = 2;
      setTimer(seq,10000);
      break;


    case 2:

      ctrl.UCapMduleMde_D_Rq = 1;   // STANDBY

      write("48V -> STANDBY");

      step = 3;
      setTimer(seq,1000);
      break;


    case 3:

      ctrl.UCapMduleMde_D_Rq = 0;   // OFF

      write("48V -> OFF");

      step = 4;
      break;
  }
}