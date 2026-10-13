

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

  int sys1 = 1;
  int sys2 = 4;
  int sys3 = 3;
  int sys4 = 2;
  int sys5 = 3;
  int sys6 = 1;

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seqTimer;

  int step = 0;
  int day = 1;

  /* ============== CAN1 ============== */

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

  /* ============== CAN2 ============== */

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

  /* ============== CAN3 ============== */

  message BCM6_BCM_CANFD::BCM_AutoSar_Network_Mgmt bcm3;
  message BCM6_BCM_CANFD::BodyInfo_3 body3;
  message BCM6_BCM_CANFD::DCDCE_AutoSar_Network_Mgmt dcdce3;
  message BCM6_BCM_CANFD::DCDCF_AutoSar_Network_Mgmt dcdcf3;
  message BCM6_BCM_CANFD::DCDCG_AutoSar_Network_Mgmt dcdcg3;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_1 ebbCtrl3;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_1 ebbInfo3;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_2 embCtrl3;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_2 embInfo3;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_3 v48Ctrl3;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_3 v48Info3;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_4 epasCtrl3;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_4 epasInfo3;

  /* ============== CAN4 ============== */

  message BCM6_BCM_CANFD::BCM_AutoSar_Network_Mgmt bcm4;
  message BCM6_BCM_CANFD::BodyInfo_3 body4;
  message BCM6_BCM_CANFD::DCDCE_AutoSar_Network_Mgmt dcdce4;
  message BCM6_BCM_CANFD::DCDCF_AutoSar_Network_Mgmt dcdcf4;
  message BCM6_BCM_CANFD::DCDCG_AutoSar_Network_Mgmt dcdcg4;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_1 ebbCtrl4;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_1 ebbInfo4;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_2 embCtrl4;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_2 embInfo4;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_3 v48Ctrl4;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_3 v48Info4;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_4 epasCtrl4;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_4 epasInfo4;

  /* ============== CAN5 ============== */

  message BCM6_BCM_CANFD::BCM_AutoSar_Network_Mgmt bcm5;
  message BCM6_BCM_CANFD::BodyInfo_3 body5;
  message BCM6_BCM_CANFD::DCDCE_AutoSar_Network_Mgmt dcdce5;
  message BCM6_BCM_CANFD::DCDCF_AutoSar_Network_Mgmt dcdcf5;
  message BCM6_BCM_CANFD::DCDCG_AutoSar_Network_Mgmt dcdcg5;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_1 ebbCtrl5;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_1 ebbInfo5;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_2 embCtrl5;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_2 embInfo5;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_3 v48Ctrl5;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_3 v48Info5;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_4 epasCtrl5;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_4 epasInfo5;

  /* ============== CAN6 ============== */

  message BCM6_BCM_CANFD::BCM_AutoSar_Network_Mgmt bcm6;
  message BCM6_BCM_CANFD::BodyInfo_3 body6;
  message BCM6_BCM_CANFD::DCDCE_AutoSar_Network_Mgmt dcdce6;
  message BCM6_BCM_CANFD::DCDCF_AutoSar_Network_Mgmt dcdcf6;
  message BCM6_BCM_CANFD::DCDCG_AutoSar_Network_Mgmt dcdcg6;

  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_1 ebbCtrl6;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_1 ebbInfo6;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_2 embCtrl6;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_2 embInfo6;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_3 v48Ctrl6;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_3 v48Info6;
  message BCM6_BCM_CANFD::EnergyMgmtBodyCtrl_4 epasCtrl6;
  message BCM6_BCM_CANFD::EnergyMgmtBodyInfo_4 epasInfo6;
}

/* ==================================================
   INITIALIZE MESSAGES
   ================================================== */

void initMessages()
{
  /* Explicit CAN channel routing */

  bcm1.CAN=1; body1.CAN=1;
  dcdce1.CAN=1; dcdcf1.CAN=1; dcdcg1.CAN=1;
  ebbCtrl1.CAN=1; ebbInfo1.CAN=1;
  embCtrl1.CAN=1; embInfo1.CAN=1;
  v48Ctrl1.CAN=1; v48Info1.CAN=1;
  epasCtrl1.CAN=1; epasInfo1.CAN=1;

  bcm2.CAN=2; body2.CAN=2;
  dcdce2.CAN=2; dcdcf2.CAN=2; dcdcg2.CAN=2;
  ebbCtrl2.CAN=2; ebbInfo2.CAN=2;
  embCtrl2.CAN=2; embInfo2.CAN=2;
  v48Ctrl2.CAN=2; v48Info2.CAN=2;
  epasCtrl2.CAN=2; epasInfo2.CAN=2;

  bcm3.CAN=3; body3.CAN=3;
  dcdce3.CAN=3; dcdcf3.CAN=3; dcdcg3.CAN=3;
  ebbCtrl3.CAN=3; ebbInfo3.CAN=3;
  embCtrl3.CAN=3; embInfo3.CAN=3;
  v48Ctrl3.CAN=3; v48Info3.CAN=3;
  epasCtrl3.CAN=3; epasInfo3.CAN=3;

  bcm4.CAN=4; body4.CAN=4;
  dcdce4.CAN=4; dcdcf4.CAN=4; dcdcg4.CAN=4;
  ebbCtrl4.CAN=4; ebbInfo4.CAN=4;
  embCtrl4.CAN=4; embInfo4.CAN=4;
  v48Ctrl4.CAN=4; v48Info4.CAN=4;
  epasCtrl4.CAN=4; epasInfo4.CAN=4;

  bcm5.CAN=5; body5.CAN=5;
  dcdce5.CAN=5; dcdcf5.CAN=5; dcdcg5.CAN=5;
  ebbCtrl5.CAN=5; ebbInfo5.CAN=5;
  embCtrl5.CAN=5; embInfo5.CAN=5;
  v48Ctrl5.CAN=5; v48Info5.CAN=5;
  epasCtrl5.CAN=5; epasInfo5.CAN=5;

  bcm6.CAN=6; body6.CAN=6;
  dcdce6.CAN=6; dcdcf6.CAN=6; dcdcg6.CAN=6;
  ebbCtrl6.CAN=6; ebbInfo6.CAN=6;
  embCtrl6.CAN=6; embInfo6.CAN=6;
  v48Ctrl6.CAN=6; v48Info6.CAN=6;
  epasCtrl6.CAN=6; epasInfo6.CAN=6;

  /* BCM default payload:
     129,0,255,255,255,255,255,255 */

  bcm1.byte(0)=129; bcm1.byte(1)=0;
  bcm1.byte(2)=255; bcm1.byte(3)=255;
  bcm1.byte(4)=255; bcm1.byte(5)=255;
  bcm1.byte(6)=255; bcm1.byte(7)=255;

  bcm2.byte(0)=129; bcm2.byte(1)=0;
  bcm2.byte(2)=255; bcm2.byte(3)=255;
  bcm2.byte(4)=255; bcm2.byte(5)=255;
  bcm2.byte(6)=255; bcm2.byte(7)=255;

  bcm3.byte(0)=129; bcm3.byte(1)=0;
  bcm3.byte(2)=255; bcm3.byte(3)=255;
  bcm3.byte(4)=255; bcm3.byte(5)=255;
  bcm3.byte(6)=255; bcm3.byte(7)=255;

  bcm4.byte(0)=129; bcm4.byte(1)=0;
  bcm4.byte(2)=255; bcm4.byte(3)=255;
  bcm4.byte(4)=255; bcm4.byte(5)=255;
  bcm4.byte(6)=255; bcm4.byte(7)=255;

  bcm5.byte(0)=129; bcm5.byte(1)=0;
  bcm5.byte(2)=255; bcm5.byte(3)=255;
  bcm5.byte(4)=255; bcm5.byte(5)=255;
  bcm5.byte(6)=255; bcm5.byte(7)=255;

  bcm6.byte(0)=129; bcm6.byte(1)=0;
  bcm6.byte(2)=255; bcm6.byte(3)=255;
  bcm6.byte(4)=255; bcm6.byte(5)=255;
  bcm6.byte(6)=255; bcm6.byte(7)=255;

  /* Network management:
     0,129,255,255,255,255,255,255 */

  dcdce1.byte(0)=0; dcdce1.byte(1)=129;
  dcdcf1.byte(0)=0; dcdcf1.byte(1)=129;
  dcdcg1.byte(0)=0; dcdcg1.byte(1)=129;

  dcdce2.byte(0)=0; dcdce2.byte(1)=129;
  dcdcf2.byte(0)=0; dcdcf2.byte(1)=129;
  dcdcg2.byte(0)=0; dcdcg2.byte(1)=129;

  dcdce3.byte(0)=0; dcdce3.byte(1)=129;
  dcdcf3.byte(0)=0; dcdcf3.byte(1)=129;
  dcdcg3.byte(0)=0; dcdcg3.byte(1)=129;

  dcdce4.byte(0)=0; dcdce4.byte(1)=129;
  dcdcf4.byte(0)=0; dcdcf4.byte(1)=129;
  dcdcg4.byte(0)=0; dcdcg4.byte(1)=129;

  dcdce5.byte(0)=0; dcdce5.byte(1)=129;
  dcdcf5.byte(0)=0; dcdcf5.byte(1)=129;
  dcdcg5.byte(0)=0; dcdcg5.byte(1)=129;

  dcdce6.byte(0)=0; dcdce6.byte(1)=129;
  dcdcf6.byte(0)=0; dcdcf6.byte(1)=129;
  dcdcg6.byte(0)=0; dcdcg6.byte(1)=129;

  /* Set remaining NM bytes to 255 */

  dcdce1.byte(2)=255; dcdce1.byte(3)=255;
  dcdce1.byte(4)=255; dcdce1.byte(5)=255;
  dcdce1.byte(6)=255; dcdce1.byte(7)=255;

  dcdcf1.byte(2)=255; dcdcf1.byte(3)=255;
  dcdcf1.byte(4)=255; dcdcf1.byte(5)=255;
  dcdcf1.byte(6)=255; dcdcf1.byte(7)=255;

  dcdcg1.byte(2)=255; dcdcg1.byte(3)=255;
  dcdcg1.byte(4)=255; dcdcg1.byte(5)=255;
  dcdcg1.byte(6)=255; dcdcg1.byte(7)=255;

  dcdce2.byte(2)=255; dcdce2.byte(3)=255;
  dcdce2.byte(4)=255; dcdce2.byte(5)=255;
  dcdce2.byte(6)=255; dcdce2.byte(7)=255;

  dcdcf2.byte(2)=255; dcdcf2.byte(3)=255;
  dcdcf2.byte(4)=255; dcdcf2.byte(5)=255;
  dcdcf2.byte(6)=255; dcdcf2.byte(7)=255;

  dcdcg2.byte(2)=255; dcdcg2.byte(3)=255;
  dcdcg2.byte(4)=255; dcdcg2.byte(5)=255;
  dcdcg2.byte(6)=255; dcdcg2.byte(7)=255;

  dcdce3.byte(2)=255; dcdce3.byte(3)=255;
  dcdce3.byte(4)=255; dcdce3.byte(5)=255;
  dcdce3.byte(6)=255; dcdce3.byte(7)=255;

  dcdcf3.byte(2)=255; dcdcf3.byte(3)=255;
  dcdcf3.byte(4)=255; dcdcf3.byte(5)=255;
  dcdcf3.byte(6)=255; dcdcf3.byte(7)=255;

  dcdcg3.byte(2)=255; dcdcg3.byte(3)=255;
  dcdcg3.byte(4)=255; dcdcg3.byte(5)=255;
  dcdcg3.byte(6)=255; dcdcg3.byte(7)=255;

  dcdce4.byte(2)=255; dcdce4.byte(3)=255;
  dcdce4.byte(4)=255; dcdce4.byte(5)=255;
  dcdce4.byte(6)=255; dcdce4.byte(7)=255;

  dcdcf4.byte(2)=255; dcdcf4.byte(3)=255;
  dcdcf4.byte(4)=255; dcdcf4.byte(5)=255;
  dcdcf4.byte(6)=255; dcdcf4.byte(7)=255;

  dcdcg4.byte(2)=255; dcdcg4.byte(3)=255;
  dcdcg4.byte(4)=255; dcdcg4.byte(5)=255;
  dcdcg4.byte(6)=255; dcdcg4.byte(7)=255;

  dcdce5.byte(2)=255; dcdce5.byte(3)=255;
  dcdce5.byte(4)=255; dcdce5.byte(5)=255;
  dcdce5.byte(6)=255; dcdce5.byte(7)=255;

  dcdcf5.byte(2)=255; dcdcf5.byte(3)=255;
  dcdcf5.byte(4)=255; dcdcf5.byte(5)=255;
  dcdcf5.byte(6)=255; dcdcf5.byte(7)=255;

  dcdcg5.byte(2)=255; dcdcg5.byte(3)=255;
  dcdcg5.byte(4)=255; dcdcg5.byte(5)=255;
  dcdcg5.byte(6)=255; dcdcg5.byte(7)=255;

  dcdce6.byte(2)=255; dcdce6.byte(3)=255;
  dcdce6.byte(4)=255; dcdce6.byte(5)=255;
  dcdce6.byte(6)=255; dcdce6.byte(7)=255;

  dcdcf6.byte(2)=255; dcdcf6.byte(3)=255;
  dcdcf6.byte(4)=255; dcdcf6.byte(5)=255;
  dcdcf6.byte(6)=255; dcdcf6.byte(7)=255;

  dcdcg6.byte(2)=255; dcdcg6.byte(3)=255;
  dcdcg6.byte(4)=255; dcdcg6.byte(5)=255;
  dcdcg6.byte(6)=255; dcdcg6.byte(7)=255;

  /* CTRL defaults: 30 168 0 13 52 192 0 0 */

  ebbCtrl1.byte(0)=30; ebbCtrl1.byte(1)=168;
  ebbCtrl1.byte(2)=0; ebbCtrl1.byte(3)=13;
  ebbCtrl1.byte(4)=52; ebbCtrl1.byte(5)=192;
  ebbCtrl1.byte(6)=0; ebbCtrl1.byte(7)=0;

  embCtrl1.byte(0)=30; embCtrl1.byte(1)=168;
  embCtrl1.byte(2)=0; embCtrl1.byte(3)=13;
  embCtrl1.byte(4)=52; embCtrl1.byte(5)=192;
  embCtrl1.byte(6)=0; embCtrl1.byte(7)=0;

  epasCtrl1.byte(0)=30; epasCtrl1.byte(1)=168;
  epasCtrl1.byte(2)=0; epasCtrl1.byte(3)=13;
  epasCtrl1.byte(4)=52; epasCtrl1.byte(5)=192;
  epasCtrl1.byte(6)=0; epasCtrl1.byte(7)=0;

  v48Ctrl1.byte(0)=254; v48Ctrl1.byte(1)=254;
  v48Ctrl1.byte(2)=254; v48Ctrl1.byte(3)=30;
  v48Ctrl1.byte(4)=0; v48Ctrl1.byte(5)=0;
  v48Ctrl1.byte(6)=0; v48Ctrl1.byte(7)=0;

  /* Copy payload defaults before channel assignment */

  ebbCtrl2=ebbCtrl1; ebbCtrl3=ebbCtrl1;
  ebbCtrl4=ebbCtrl1; ebbCtrl5=ebbCtrl1;
  ebbCtrl6=ebbCtrl1;

  embCtrl2=embCtrl1; embCtrl3=embCtrl1;
  embCtrl4=embCtrl1; embCtrl5=embCtrl1;
  embCtrl6=embCtrl1;

  epasCtrl2=epasCtrl1; epasCtrl3=epasCtrl1;
  epasCtrl4=epasCtrl1; epasCtrl5=epasCtrl1;
  epasCtrl6=epasCtrl1;

  v48Ctrl2=v48Ctrl1; v48Ctrl3=v48Ctrl1;
  v48Ctrl4=v48Ctrl1; v48Ctrl5=v48Ctrl1;
  v48Ctrl6=v48Ctrl1;

  /* INFO defaults */

  ebbInfo1.byte(0)=0; ebbInfo1.byte(1)=0;
  ebbInfo1.byte(2)=0; ebbInfo1.byte(3)=0;
  ebbInfo1.byte(4)=0; ebbInfo1.byte(5)=0;
  ebbInfo1.byte(6)=162; ebbInfo1.byte(7)=128;

  embInfo1.byte(0)=0; embInfo1.byte(1)=0;
  embInfo1.byte(2)=0; embInfo1.byte(3)=0;
  embInfo1.byte(4)=0; embInfo1.byte(5)=0;
  embInfo1.byte(6)=162; embInfo1.byte(7)=128;

  epasInfo1.byte(0)=0; epasInfo1.byte(1)=0;
  epasInfo1.byte(2)=0; epasInfo1.byte(3)=0;
  epasInfo1.byte(4)=0; epasInfo1.byte(5)=0;
  epasInfo1.byte(6)=162; epasInfo1.byte(7)=128;

  v48Info1.byte(0)=8;
  v48Info1.byte(1)=254;
  v48Info1.byte(2)=254;
  v48Info1.byte(3)=0;
  v48Info1.byte(4)=0;
  v48Info1.byte(5)=0;
  v48Info1.byte(6)=0;
  v48Info1.byte(7)=0;

  ebbInfo2=ebbInfo1; ebbInfo3=ebbInfo1;
  ebbInfo4=ebbInfo1; ebbInfo5=ebbInfo1;
  ebbInfo6=ebbInfo1;

  embInfo2=embInfo1; embInfo3=embInfo1;
  embInfo4=embInfo1; embInfo5=embInfo1;
  embInfo6=embInfo1;

  epasInfo2=epasInfo1; epasInfo3=epasInfo1;
  epasInfo4=epasInfo1; epasInfo5=epasInfo1;
  epasInfo6=epasInfo1;

  v48Info2=v48Info1; v48Info3=v48Info1;
  v48Info4=v48Info1; v48Info5=v48Info1;
  v48Info6=v48Info1;

  /* Reapply channel routing after copies */

  ebbCtrl1.CAN=1; ebbInfo1.CAN=1;
  embCtrl1.CAN=1; embInfo1.CAN=1;
  epasCtrl1.CAN=1; epasInfo1.CAN=1;
  v48Ctrl1.CAN=1; v48Info1.CAN=1;

  ebbCtrl2.CAN=2; ebbInfo2.CAN=2;
  embCtrl2.CAN=2; embInfo2.CAN=2;
  epasCtrl2.CAN=2; epasInfo2.CAN=2;
  v48Ctrl2.CAN=2; v48Info2.CAN=2;

  ebbCtrl3.CAN=3; ebbInfo3.CAN=3;
  embCtrl3.CAN=3; embInfo3.CAN=3;
  epasCtrl3.CAN=3; epasInfo3.CAN=3;
  v48Ctrl3.CAN=3; v48Info3.CAN=3;

  ebbCtrl4.CAN=4; ebbInfo4.CAN=4;
  embCtrl4.CAN=4; embInfo4.CAN=4;
  epasCtrl4.CAN=4; epasInfo4.CAN=4;
  v48Ctrl4.CAN=4; v48Info4.CAN=4;

  ebbCtrl5.CAN=5; ebbInfo5.CAN=5;
  embCtrl5.CAN=5; embInfo5.CAN=5;
  epasCtrl5.CAN=5; epasInfo5.CAN=5;
  v48Ctrl5.CAN=5; v48Info5.CAN=5;

  ebbCtrl6.CAN=6; ebbInfo6.CAN=6;
  embCtrl6.CAN=6; embInfo6.CAN=6;
  epasCtrl6.CAN=6; epasInfo6.CAN=6;
  v48Ctrl6.CAN=6; v48Info6.CAN=6;

  /* BodyInfo ignition RUN and Parklamp ON */

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

/* ==================================================
   MODE CONTROL
   OFF=0, STANDBY=1, FLOAT=3
   ================================================== */

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

/* ==================================================
   ISOLATION
   OPEN=0, CLOSE=1
   NO ISOLATION FOR 48V EPAS
   ================================================== */

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

/* ==================================================
   CONTROL + INFO EVERY 100 MS
   ================================================== */

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

/* ==================================================
   BODY INFO EVERY 500 MS
   ================================================== */

void send500()
{
  if(sys1!=0) output(body1);
  if(sys2!=0) output(body2);
  if(sys3!=0) output(body3);
  if(sys4!=0) output(body4);
  if(sys5!=0) output(body5);
  if(sys6!=0) output(body6);
}

/* ==================================================
   NETWORK MANAGEMENT EVERY 1000 MS
   ================================================== */

void send1000()
{
  if(sys1!=0) output(bcm1);
  if(sys2!=0) output(bcm2);
  if(sys3!=0) output(bcm3);
  if(sys4!=0) output(bcm4);
  if(sys5!=0) output(bcm5);
  if(sys6!=0) output(bcm6);

  /* EBB: DCDCF + DCDCG */

  if(sys1==1) { output(dcdcf1); output(dcdcg1); }
  if(sys2==1) { output(dcdcf2); output(dcdcg2); }
  if(sys3==1) { output(dcdcf3); output(dcdcg3); }
  if(sys4==1) { output(dcdcf4); output(dcdcg4); }
  if(sys5==1) { output(dcdcf5); output(dcdcg5); }
  if(sys6==1) { output(dcdcf6); output(dcdcg6); }

  /* EMB: DCDCE + DCDCF */

  if(sys1==2) { output(dcdce1); output(dcdcf1); }
  if(sys2==2) { output(dcdce2); output(dcdcf2); }
  if(sys3==2) { output(dcdce3); output(dcdcf3); }
  if(sys4==2) { output(dcdce4); output(dcdcf4); }
  if(sys5==2) { output(dcdce5); output(dcdcf5); }
  if(sys6==2) { output(dcdce6); output(dcdcf6); }

  /* 48V EPAS: DCDCE + DCDCG */

  if(sys1==3) { output(dcdce1); output(dcdcg1); }
  if(sys2==3) { output(dcdce2); output(dcdcg2); }
  if(sys3==3) { output(dcdce3); output(dcdcg3); }
  if(sys4==3) { output(dcdce4); output(dcdcg4); }
  if(sys5==3) { output(dcdce5); output(dcdcg5); }
  if(sys6==3) { output(dcdce6); output(dcdcg6); }

  /* 12V EPAS: DCDCG */

  if(sys1==4) output(dcdcg1);
  if(sys2==4) output(dcdcg2);
  if(sys3==4) output(dcdcg3);
  if(sys4==4) output(dcdcg4);
  if(sys5==4) output(dcdcg5);
  if(sys6==4) output(dcdcg6);
}

/* ==================================================
   STARTUP
   OFF 2 SEC
   STANDBY 2 SEC
   ================================================== */

on start
{
  initMessages();

  step=0;
  day=1;

  setMode(0);
  setIsolation(1);

  send100();
  send500();
  send1000();

  setTimer(t100,100);
  setTimer(t500,500);
  setTimer(t1000,1000);

  write("START - OFF - 2 SEC");
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

/* ==================================================
   FIVE DAY SEQUENCE

   EACH DAY:
   FLOAT 18 HOURS TOTAL
     FIRST 1 SEC ISOLATION OPEN
     REMAINING 17H 59M 59S CLOSED
   STANDBY 6 HOURS

   REPEAT FIVE TIMES
   ================================================== */

on timer seqTimer
{
  /* OFF completed */

  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("STARTUP - STANDBY - 2 SEC");

    step=1;
    setTimer(seqTimer,2000);
  }

  /* Enter FLOAT */

  else if(step==1)
  {
    setMode(3);
    setIsolation(0);

    write("DAY %d - FLOAT - ISOLATION OPEN",day);

    step=2;
    setTimer(seqTimer,1000);
  }

  /* Close isolation, continue FLOAT */

  else if(step==2)
  {
    setIsolation(1);

    write("DAY %d - ISOLATION CLOSE",day);

    step=3;
    setTimer(seqTimer,64799000);
  }

  /* FLOAT complete, enter STANDBY */

  else if(step==3)
  {
    setMode(1);
    setIsolation(1);

    write("DAY %d - STANDBY 6 HOURS",day);

    step=4;
    setTimer(seqTimer,21600000);
  }

  /* STANDBY complete */

  else if(step==4)
  {
    if(day<5)
    {
      day=day+1;

      setMode(3);
      setIsolation(0);

      write("DAY %d - FLOAT - ISOLATION OPEN",day);

      step=2;
      setTimer(seqTimer,1000);
    }
    else
    {
      cancelTimer(t100);
      cancelTimer(t500);
      cancelTimer(t1000);

      write("FIVE DAY TEST COMPLETE");
      write("120 HOURS FINISHED");
      write("STOP MEASUREMENT");

      stop();
    }
  }
}
