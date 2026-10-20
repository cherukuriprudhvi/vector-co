
/*@!Encoding:1252*/

variables
{
  /* =========================================================
     SYSTEM SELECTION
     0 = NONE
     1 = EBB
     2 = EMB
     3 = 48V EPAS
     4 = 12V EPAS
     ========================================================= */

  int sys1 = 0;
  int sys2 = 0;
  int sys3 = 0;
  int sys4 = 0;
  int sys5 = 0;
  int sys6 = 0;

  int testRunning = 0;
  int step = 0;

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seqTimer;


  /* =========================================================
     CAN 1
     ========================================================= */

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


  /* =========================================================
     CAN 2
     ========================================================= */

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


  /* =========================================================
     CAN 3
     ========================================================= */

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


  /* =========================================================
     CAN 4
     ========================================================= */

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


  /* =========================================================
     CAN 5
     ========================================================= */

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


  /* =========================================================
     CAN 6
     ========================================================= */

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


/* ============================================================
   INITIALIZE STATIC VALUES
   ============================================================ */

void initMessages()
{
  /* ================= BCM ================= */

  bcm1.BCM_AutoSarNMNodeId = 129;
  bcm1.BCM_AutoSarNMControl = 0;
  bcm1.BCM_AutoSarNMReserved1 = 255;
  bcm1.BCM_AutoSarNMReserved2 = 255;
  bcm1.BCM_GWOnBoardTester = 255;
  bcm1.BCM_GWNMProxy = 255;
  bcm1.BCM_AutoSarNMReserved3 = 255;
  bcm1.BCM_AutoSarNMReserved4 = 255;

  bcm2.BCM_AutoSarNMNodeId = 129;
  bcm2.BCM_AutoSarNMControl = 0;
  bcm2.BCM_AutoSarNMReserved1 = 255;
  bcm2.BCM_AutoSarNMReserved2 = 255;
  bcm2.BCM_GWOnBoardTester = 255;
  bcm2.BCM_GWNMProxy = 255;
  bcm2.BCM_AutoSarNMReserved3 = 255;
  bcm2.BCM_AutoSarNMReserved4 = 255;

  bcm3.BCM_AutoSarNMNodeId = 129;
  bcm3.BCM_AutoSarNMControl = 0;
  bcm3.BCM_AutoSarNMReserved1 = 255;
  bcm3.BCM_AutoSarNMReserved2 = 255;
  bcm3.BCM_GWOnBoardTester = 255;
  bcm3.BCM_GWNMProxy = 255;
  bcm3.BCM_AutoSarNMReserved3 = 255;
  bcm3.BCM_AutoSarNMReserved4 = 255;

  bcm4.BCM_AutoSarNMNodeId = 129;
  bcm4.BCM_AutoSarNMControl = 0;
  bcm4.BCM_AutoSarNMReserved1 = 255;
  bcm4.BCM_AutoSarNMReserved2 = 255;
  bcm4.BCM_GWOnBoardTester = 255;
  bcm4.BCM_GWNMProxy = 255;
  bcm4.BCM_AutoSarNMReserved3 = 255;
  bcm4.BCM_AutoSarNMReserved4 = 255;

  bcm5.BCM_AutoSarNMNodeId = 129;
  bcm5.BCM_AutoSarNMControl = 0;
  bcm5.BCM_AutoSarNMReserved1 = 255;
  bcm5.BCM_AutoSarNMReserved2 = 255;
  bcm5.BCM_GWOnBoardTester = 255;
  bcm5.BCM_GWNMProxy = 255;
  bcm5.BCM_AutoSarNMReserved3 = 255;
  bcm5.BCM_AutoSarNMReserved4 = 255;

  bcm6.BCM_AutoSarNMNodeId = 129;
  bcm6.BCM_AutoSarNMControl = 0;
  bcm6.BCM_AutoSarNMReserved1 = 255;
  bcm6.BCM_AutoSarNMReserved2 = 255;
  bcm6.BCM_GWOnBoardTester = 255;
  bcm6.BCM_GWNMProxy = 255;
  bcm6.BCM_AutoSarNMReserved3 = 255;
  bcm6.BCM_AutoSarNMReserved4 = 255;


  /* ================= NM CAN1 ================= */

  dcdce1.DCDCE_AutoSarNMControl=0;
  dcdce1.DCDCE_AutoSarNMNodeId=129;
  dcdce1.DCDCE_AutoSarNMReserved1=255;
  dcdce1.DCDCE_AutoSarNMReserved2=255;
  dcdce1.DCDCE_GWOnBoardTester=255;
  dcdce1.DCDCE_GWNMProxy=255;
  dcdce1.DCDCE_AutoSarNMReserved3=255;
  dcdce1.DCDCE_AutoSarNMReserved4=255;

  dcdcf1.DCDCF_AutoSarNMControl=0;
  dcdcf1.DCDCF_AutoSarNMNodeId=129;
  dcdcf1.DCDCF_AutoSarNMReserved1=255;
  dcdcf1.DCDCF_AutoSarNMReserved2=255;
  dcdcf1.DCDCF_GWOnBoardTester=255;
  dcdcf1.DCDCF_GWNMProxy=255;
  dcdcf1.DCDCF_AutoSarNMReserved3=255;
  dcdcf1.DCDCF_AutoSarNMReserved4=255;

  dcdcg1.DCDCG_AutoSarNMControl=0;
  dcdcg1.DCDCG_AutoSarNMNodeId=129;
  dcdcg1.DCDCG_AutoSarNMReserved1=255;
  dcdcg1.DCDCG_AutoSarNMReserved2=255;
  dcdcg1.DCDCG_GWOnBoardTester=255;
  dcdcg1.DCDCG_GWNMProxy=255;
  dcdcg1.DCDCG_AutoSarNMReserved3=255;
  dcdcg1.DCDCG_AutoSarNMReserved4=255;


  /* ================= NM CAN2-CAN6 ================= */

  dcdce2.byte(0)=0; dcdce2.byte(1)=129;
  dcdce2.byte(2)=255; dcdce2.byte(3)=255;
  dcdce2.byte(4)=255; dcdce2.byte(5)=255;
  dcdce2.byte(6)=255; dcdce2.byte(7)=255;

  dcdce3.byte(0)=0; dcdce3.byte(1)=129;
  dcdce3.byte(2)=255; dcdce3.byte(3)=255;
  dcdce3.byte(4)=255; dcdce3.byte(5)=255;
  dcdce3.byte(6)=255; dcdce3.byte(7)=255;

  dcdce4.byte(0)=0; dcdce4.byte(1)=129;
  dcdce4.byte(2)=255; dcdce4.byte(3)=255;
  dcdce4.byte(4)=255; dcdce4.byte(5)=255;
  dcdce4.byte(6)=255; dcdce4.byte(7)=255;

  dcdce5.byte(0)=0; dcdce5.byte(1)=129;
  dcdce5.byte(2)=255; dcdce5.byte(3)=255;
  dcdce5.byte(4)=255; dcdce5.byte(5)=255;
  dcdce5.byte(6)=255; dcdce5.byte(7)=255;

  dcdce6.byte(0)=0; dcdce6.byte(1)=129;
  dcdce6.byte(2)=255; dcdce6.byte(3)=255;
  dcdce6.byte(4)=255; dcdce6.byte(5)=255;
  dcdce6.byte(6)=255; dcdce6.byte(7)=255;


  dcdcf2.byte(0)=0; dcdcf2.byte(1)=129;
  dcdcf2.byte(2)=255; dcdcf2.byte(3)=255;
  dcdcf2.byte(4)=255; dcdcf2.byte(5)=255;
  dcdcf2.byte(6)=255; dcdcf2.byte(7)=255;

  dcdcf3.byte(0)=0; dcdcf3.byte(1)=129;
  dcdcf3.byte(2)=255; dcdcf3.byte(3)=255;
  dcdcf3.byte(4)=255; dcdcf3.byte(5)=255;
  dcdcf3.byte(6)=255; dcdcf3.byte(7)=255;

  dcdcf4.byte(0)=0; dcdcf4.byte(1)=129;
  dcdcf4.byte(2)=255; dcdcf4.byte(3)=255;
  dcdcf4.byte(4)=255; dcdcf4.byte(5)=255;
  dcdcf4.byte(6)=255; dcdcf4.byte(7)=255;

  dcdcf5.byte(0)=0; dcdcf5.byte(1)=129;
  dcdcf5.byte(2)=255; dcdcf5.byte(3)=255;
  dcdcf5.byte(4)=255; dcdcf5.byte(5)=255;
  dcdcf5.byte(6)=255; dcdcf5.byte(7)=255;

  dcdcf6.byte(0)=0; dcdcf6.byte(1)=129;
  dcdcf6.byte(2)=255; dcdcf6.byte(3)=255;
  dcdcf6.byte(4)=255; dcdcf6.byte(5)=255;
  dcdcf6.byte(6)=255; dcdcf6.byte(7)=255;


  dcdcg2.byte(0)=0; dcdcg2.byte(1)=129;
  dcdcg2.byte(2)=255; dcdcg2.byte(3)=255;
  dcdcg2.byte(4)=255; dcdcg2.byte(5)=255;
  dcdcg2.byte(6)=255; dcdcg2.byte(7)=255;

  dcdcg3.byte(0)=0; dcdcg3.byte(1)=129;
  dcdcg3.byte(2)=255; dcdcg3.byte(3)=255;
  dcdcg3.byte(4)=255; dcdcg3.byte(5)=255;
  dcdcg3.byte(6)=255; dcdcg3.byte(7)=255;

  dcdcg4.byte(0)=0; dcdcg4.byte(1)=129;
  dcdcg4.byte(2)=255; dcdcg4.byte(3)=255;
  dcdcg4.byte(4)=255; dcdcg4.byte(5)=255;
  dcdcg4.byte(6)=255; dcdcg4.byte(7)=255;

  dcdcg5.byte(0)=0; dcdcg5.byte(1)=129;
  dcdcg5.byte(2)=255; dcdcg5.byte(3)=255;
  dcdcg5.byte(4)=255; dcdcg5.byte(5)=255;
  dcdcg5.byte(6)=255; dcdcg5.byte(7)=255;

  dcdcg6.byte(0)=0; dcdcg6.byte(1)=129;
  dcdcg6.byte(2)=255; dcdcg6.byte(3)=255;
  dcdcg6.byte(4)=255; dcdcg6.byte(5)=255;
  dcdcg6.byte(6)=255; dcdcg6.byte(7)=255;


  /* ================= CONTROL DEFAULTS ================= */

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


  /* ================= CONTROL CAN2-CAN6 ================= */

  ebbCtrl2.byte(0)=30; ebbCtrl2.byte(1)=168;
  ebbCtrl2.byte(2)=0;  ebbCtrl2.byte(3)=13;
  ebbCtrl2.byte(4)=52; ebbCtrl2.byte(5)=192;
  ebbCtrl2.byte(6)=0;  ebbCtrl2.byte(7)=0;

  ebbCtrl3.byte(0)=30; ebbCtrl3.byte(1)=168;
  ebbCtrl3.byte(2)=0;  ebbCtrl3.byte(3)=13;
  ebbCtrl3.byte(4)=52; ebbCtrl3.byte(5)=192;
  ebbCtrl3.byte(6)=0;  ebbCtrl3.byte(7)=0;

  ebbCtrl4.byte(0)=30; ebbCtrl4.byte(1)=168;
  ebbCtrl4.byte(2)=0;  ebbCtrl4.byte(3)=13;
  ebbCtrl4.byte(4)=52; ebbCtrl4.byte(5)=192;
  ebbCtrl4.byte(6)=0;  ebbCtrl4.byte(7)=0;

  ebbCtrl5.byte(0)=30; ebbCtrl5.byte(1)=168;
  ebbCtrl5.byte(2)=0;  ebbCtrl5.byte(3)=13;
  ebbCtrl5.byte(4)=52; ebbCtrl5.byte(5)=192;
  ebbCtrl5.byte(6)=0;  ebbCtrl5.byte(7)=0;

  ebbCtrl6.byte(0)=30; ebbCtrl6.byte(1)=168;
  ebbCtrl6.byte(2)=0;  ebbCtrl6.byte(3)=13;
  ebbCtrl6.byte(4)=52; ebbCtrl6.byte(5)=192;
  ebbCtrl6.byte(6)=0;  ebbCtrl6.byte(7)=0;


  embCtrl2.byte(0)=30; embCtrl2.byte(1)=168;
  embCtrl2.byte(2)=0;  embCtrl2.byte(3)=13;
  embCtrl2.byte(4)=52; embCtrl2.byte(5)=192;
  embCtrl2.byte(6)=0;  embCtrl2.byte(7)=0;

  embCtrl3.byte(0)=30; embCtrl3.byte(1)=168;
  embCtrl3.byte(2)=0;  embCtrl3.byte(3)=13;
  embCtrl3.byte(4)=52; embCtrl3.byte(5)=192;
  embCtrl3.byte(6)=0;  embCtrl3.byte(7)=0;

  embCtrl4.byte(0)=30; embCtrl4.byte(1)=168;
  embCtrl4.byte(2)=0;  embCtrl4.byte(3)=13;
  embCtrl4.byte(4)=52; embCtrl4.byte(5)=192;
  embCtrl4.byte(6)=0;  embCtrl4.byte(7)=0;

  embCtrl5.byte(0)=30; embCtrl5.byte(1)=168;
  embCtrl5.byte(2)=0;  embCtrl5.byte(3)=13;
  embCtrl5.byte(4)=52; embCtrl5.byte(5)=192;
  embCtrl5.byte(6)=0;  embCtrl5.byte(7)=0;

  embCtrl6.byte(0)=30; embCtrl6.byte(1)=168;
  embCtrl6.byte(2)=0;  embCtrl6.byte(3)=13;
  embCtrl6.byte(4)=52; embCtrl6.byte(5)=192;
  embCtrl6.byte(6)=0;  embCtrl6.byte(7)=0;


  epasCtrl2.byte(0)=30; epasCtrl2.byte(1)=168;
  epasCtrl2.byte(2)=0;  epasCtrl2.byte(3)=13;
  epasCtrl2.byte(4)=52; epasCtrl2.byte(5)=192;
  epasCtrl2.byte(6)=0;  epasCtrl2.byte(7)=0;

  epasCtrl3.byte(0)=30; epasCtrl3.byte(1)=168;
  epasCtrl3.byte(2)=0;  epasCtrl3.byte(3)=13;
  epasCtrl3.byte(4)=52; epasCtrl3.byte(5)=192;
  epasCtrl3.byte(6)=0;  epasCtrl3.byte(7)=0;

  epasCtrl4.byte(0)=30; epasCtrl4.byte(1)=168;
  epasCtrl4.byte(2)=0;  epasCtrl4.byte(3)=13;
  epasCtrl4.byte(4)=52; epasCtrl4.byte(5)=192;
  epasCtrl4.byte(6)=0;  epasCtrl4.byte(7)=0;

  epasCtrl5.byte(0)=30; epasCtrl5.byte(1)=168;
  epasCtrl5.byte(2)=0;  epasCtrl5.byte(3)=13;
  epasCtrl5.byte(4)=52; epasCtrl5.byte(5)=192;
  epasCtrl5.byte(6)=0;  epasCtrl5.byte(7)=0;

  epasCtrl6.byte(0)=30; epasCtrl6.byte(1)=168;
  epasCtrl6.byte(2)=0;  epasCtrl6.byte(3)=13;
  epasCtrl6.byte(4)=52; epasCtrl6.byte(5)=192;
  epasCtrl6.byte(6)=0;  epasCtrl6.byte(7)=0;


  v48Ctrl2.byte(0)=254; v48Ctrl2.byte(1)=254;
  v48Ctrl2.byte(2)=254; v48Ctrl2.byte(3)=30;
  v48Ctrl2.byte(4)=0; v48Ctrl2.byte(5)=0;
  v48Ctrl2.byte(6)=0; v48Ctrl2.byte(7)=0;

  v48Ctrl3.byte(0)=254; v48Ctrl3.byte(1)=254;
  v48Ctrl3.byte(2)=254; v48Ctrl3.byte(3)=30;
  v48Ctrl3.byte(4)=0; v48Ctrl3.byte(5)=0;
  v48Ctrl3.byte(6)=0; v48Ctrl3.byte(7)=0;

  v48Ctrl4.byte(0)=254; v48Ctrl4.byte(1)=254;
  v48Ctrl4.byte(2)=254; v48Ctrl4.byte(3)=30;
  v48Ctrl4.byte(4)=0; v48Ctrl4.byte(5)=0;
  v48Ctrl4.byte(6)=0; v48Ctrl4.byte(7)=0;

  v48Ctrl5.byte(0)=254; v48Ctrl5.byte(1)=254;
  v48Ctrl5.byte(2)=254; v48Ctrl5.byte(3)=30;
  v48Ctrl5.byte(4)=0; v48Ctrl5.byte(5)=0;
  v48Ctrl5.byte(6)=0; v48Ctrl5.byte(7)=0;

  v48Ctrl6.byte(0)=254; v48Ctrl6.byte(1)=254;
  v48Ctrl6.byte(2)=254; v48Ctrl6.byte(3)=30;
  v48Ctrl6.byte(4)=0; v48Ctrl6.byte(5)=0;
  v48Ctrl6.byte(6)=0; v48Ctrl6.byte(7)=0;


  /* ================= INFO DEFAULTS ================= */

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


  /* INFO CAN2-CAN6 */

  ebbInfo2.byte(0)=0; ebbInfo2.byte(1)=0;
  ebbInfo2.byte(2)=0; ebbInfo2.byte(3)=0;
  ebbInfo2.byte(4)=0; ebbInfo2.byte(5)=0;
  ebbInfo2.byte(6)=162; ebbInfo2.byte(7)=128;

  ebbInfo3.byte(0)=0; ebbInfo3.byte(1)=0;
  ebbInfo3.byte(2)=0; ebbInfo3.byte(3)=0;
  ebbInfo3.byte(4)=0; ebbInfo3.byte(5)=0;
  ebbInfo3.byte(6)=162; ebbInfo3.byte(7)=128;

  ebbInfo4.byte(0)=0; ebbInfo4.byte(1)=0;
  ebbInfo4.byte(2)=0; ebbInfo4.byte(3)=0;
  ebbInfo4.byte(4)=0; ebbInfo4.byte(5)=0;
  ebbInfo4.byte(6)=162; ebbInfo4.byte(7)=128;

  ebbInfo5.byte(0)=0; ebbInfo5.byte(1)=0;
  ebbInfo5.byte(2)=0; ebbInfo5.byte(3)=0;
  ebbInfo5.byte(4)=0; ebbInfo5.byte(5)=0;
  ebbInfo5.byte(6)=162; ebbInfo5.byte(7)=128;

  ebbInfo6.byte(0)=0; ebbInfo6.byte(1)=0;
  ebbInfo6.byte(2)=0; ebbInfo6.byte(3)=0;
  ebbInfo6.byte(4)=0; ebbInfo6.byte(5)=0;
  ebbInfo6.byte(6)=162; ebbInfo6.byte(7)=128;


  embInfo2.byte(0)=0; embInfo2.byte(1)=0;
  embInfo2.byte(2)=0; embInfo2.byte(3)=0;
  embInfo2.byte(4)=0; embInfo2.byte(5)=0;
  embInfo2.byte(6)=162; embInfo2.byte(7)=128;

  embInfo3.byte(0)=0; embInfo3.byte(1)=0;
  embInfo3.byte(2)=0; embInfo3.byte(3)=0;
  embInfo3.byte(4)=0; embInfo3.byte(5)=0;
  embInfo3.byte(6)=162; embInfo3.byte(7)=128;

  embInfo4.byte(0)=0; embInfo4.byte(1)=0;
  embInfo4.byte(2)=0; embInfo4.byte(3)=0;
  embInfo4.byte(4)=0; embInfo4.byte(5)=0;
  embInfo4.byte(6)=162; embInfo4.byte(7)=128;

  embInfo5.byte(0)=0; embInfo5.byte(1)=0;
  embInfo5.byte(2)=0; embInfo5.byte(3)=0;
  embInfo5.byte(4)=0; embInfo5.byte(5)=0;
  embInfo5.byte(6)=162; embInfo5.byte(7)=128;

  embInfo6.byte(0)=0; embInfo6.byte(1)=0;
  embInfo6.byte(2)=0; embInfo6.byte(3)=0;
  embInfo6.byte(4)=0; embInfo6.byte(5)=0;
  embInfo6.byte(6)=162; embInfo6.byte(7)=128;


  epasInfo2.byte(0)=0; epasInfo2.byte(1)=0;
  epasInfo2.byte(2)=0; epasInfo2.byte(3)=0;
  epasInfo2.byte(4)=0; epasInfo2.byte(5)=0;
  epasInfo2.byte(6)=162; epasInfo2.byte(7)=128;

  epasInfo3.byte(0)=0; epasInfo3.byte(1)=0;
  epasInfo3.byte(2)=0; epasInfo3.byte(3)=0;
  epasInfo3.byte(4)=0; epasInfo3.byte(5)=0;
  epasInfo3.byte(6)=162; epasInfo3.byte(7)=128;

  epasInfo4.byte(0)=0; epasInfo4.byte(1)=0;
  epasInfo4.byte(2)=0; epasInfo4.byte(3)=0;
  epasInfo4.byte(4)=0; epasInfo4.byte(5)=0;
  epasInfo4.byte(6)=162; epasInfo4.byte(7)=128;

  epasInfo5.byte(0)=0; epasInfo5.byte(1)=0;
  epasInfo5.byte(2)=0; epasInfo5.byte(3)=0;
  epasInfo5.byte(4)=0; epasInfo5.byte(5)=0;
  epasInfo5.byte(6)=162; epasInfo5.byte(7)=128;

  epasInfo6.byte(0)=0; epasInfo6.byte(1)=0;
  epasInfo6.byte(2)=0; epasInfo6.byte(3)=0;
  epasInfo6.byte(4)=0; epasInfo6.byte(5)=0;
  epasInfo6.byte(6)=162; epasInfo6.byte(7)=128;


  v48Info2.byte(0)=8; v48Info2.byte(1)=254;
  v48Info2.byte(2)=254; v48Info2.byte(3)=0;
  v48Info2.byte(4)=0; v48Info2.byte(5)=0;
  v48Info2.byte(6)=0; v48Info2.byte(7)=0;

  v48Info3.byte(0)=8; v48Info3.byte(1)=254;
  v48Info3.byte(2)=254; v48Info3.byte(3)=0;
  v48Info3.byte(4)=0; v48Info3.byte(5)=0;
  v48Info3.byte(6)=0; v48Info3.byte(7)=0;

  v48Info4.byte(0)=8; v48Info4.byte(1)=254;
  v48Info4.byte(2)=254; v48Info4.byte(3)=0;
  v48Info4.byte(4)=0; v48Info4.byte(5)=0;
  v48Info4.byte(6)=0; v48Info4.byte(7)=0;

  v48Info5.byte(0)=8; v48Info5.byte(1)=254;
  v48Info5.byte(2)=254; v48Info5.byte(3)=0;
  v48Info5.byte(4)=0; v48Info5.byte(5)=0;
  v48Info5.byte(6)=0; v48Info5.byte(7)=0;

  v48Info6.byte(0)=8; v48Info6.byte(1)=254;
  v48Info6.byte(2)=254; v48Info6.byte(3)=0;
  v48Info6.byte(4)=0; v48Info6.byte(5)=0;
  v48Info6.byte(6)=0; v48Info6.byte(7)=0;


  /* ================= BODY INFO ================= */

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


/* ============================================================
   MODE CONTROL
   0 = OFF
   1 = STANDBY
   3 = FLOAT
   ============================================================ */

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


/* ============================================================
   ISOLATION CONTROL
   0 = OPEN
   1 = CLOSE

   48V EPAS = NO ISOLATION COMMAND
   ============================================================ */

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


/* ============================================================
   100 ms TRANSMISSION
   ============================================================ */

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


/* ============================================================
   500 ms TRANSMISSION
   ============================================================ */

void send500()
{
  if(sys1!=0) output(body1);
  if(sys2!=0) output(body2);
  if(sys3!=0) output(body3);
  if(sys4!=0) output(body4);
  if(sys5!=0) output(body5);
  if(sys6!=0) output(body6);
}


/* ============================================================
   1000 ms TRANSMISSION
   ============================================================ */

void send1000()
{
  /* BCM */

  if(sys1!=0) output(bcm1);
  if(sys2!=0) output(bcm2);
  if(sys3!=0) output(bcm3);
  if(sys4!=0) output(bcm4);
  if(sys5!=0) output(bcm5);
  if(sys6!=0) output(bcm6);


  /* EBB = DCDCF + DCDCG */

  if(sys1==1) { output(dcdcf1); output(dcdcg1); }
  if(sys2==1) { output(dcdcf2); output(dcdcg2); }
  if(sys3==1) { output(dcdcf3); output(dcdcg3); }
  if(sys4==1) { output(dcdcf4); output(dcdcg4); }
  if(sys5==1) { output(dcdcf5); output(dcdcg5); }
  if(sys6==1) { output(dcdcf6); output(dcdcg6); }


  /* EMB = DCDCE + DCDCF */

  if(sys1==2) { output(dcdce1); output(dcdcf1); }
  if(sys2==2) { output(dcdce2); output(dcdcf2); }
  if(sys3==2) { output(dcdce3); output(dcdcf3); }
  if(sys4==2) { output(dcdce4); output(dcdcf4); }
  if(sys5==2) { output(dcdce5); output(dcdcf5); }
  if(sys6==2) { output(dcdce6); output(dcdcf6); }


  /* 48V EPAS = DCDCE + DCDCG */

  if(sys1==3) { output(dcdce1); output(dcdcg1); }
  if(sys2==3) { output(dcdce2); output(dcdcg2); }
  if(sys3==3) { output(dcdce3); output(dcdcg3); }
  if(sys4==3) { output(dcdce4); output(dcdcg4); }
  if(sys5==3) { output(dcdce5); output(dcdcg5); }
  if(sys6==3) { output(dcdce6); output(dcdcg6); }


  /* 12V EPAS = DCDCG */

  if(sys1==4) output(dcdcg1);
  if(sys2==4) output(dcdcg2);
  if(sys3==4) output(dcdcg3);
  if(sys4==4) output(dcdcg4);
  if(sys5==4) output(dcdcg5);
  if(sys6==4) output(dcdcg6);
}


/* ============================================================
   MEASUREMENT START

   F9 ONLY STARTS MEASUREMENT.
   TEST WAITS FOR PANEL START TEST.
   ============================================================ */

on start
{
  sys1=0;
  sys2=0;
  sys3=0;
  sys4=0;
  sys5=0;
  sys6=0;

  step=0;
  testRunning=0;

  @sysvar::MasterCtrl::StartTest = 0;
  @sysvar::MasterCtrl::StopTest = 0;

  write("MEASUREMENT STARTED - WAITING FOR PANEL START TEST");
}


/* ============================================================
   PANEL START TEST
   ============================================================ */

on sysvar MasterCtrl::StartTest
{
  if(@this == 1 && testRunning == 0)
  {
    sys1 = @sysvar::CH1::Module;
    sys2 = @sysvar::CH2::Module;
    sys3 = @sysvar::CH3::Module;
    sys4 = @sysvar::CH4::Module;
    sys5 = @sysvar::CH5::Module;
    sys6 = @sysvar::CH6::Module;

    if(sys1==0 && sys2==0 && sys3==0 &&
       sys4==0 && sys5==0 && sys6==0)
    {
      write("START REJECTED - NO SYSTEM SELECTED");
      @sysvar::MasterCtrl::StartTest = 0;
      return;
    }

    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);

    testRunning=1;
    step=0;

    initMessages();

    setMode(0);
    setIsolation(1);

    send100();
    send500();
    send1000();

    setTimer(t100,100);
    setTimer(t500,500);
    setTimer(t1000,1000);

    write("==========================================");
    write("PANEL START TEST");
    write("CAN1=%d CAN2=%d CAN3=%d",sys1,sys2,sys3);
    write("CAN4=%d CAN5=%d CAN6=%d",sys4,sys5,sys6);
    write("START - OFF - 2 SEC");
    write("==========================================");

    setTimer(seqTimer,2000);

    @sysvar::MasterCtrl::StartTest = 0;
  }
}


/* ============================================================
   PANEL STOP TEST
   ============================================================ */

on sysvar MasterCtrl::StopTest
{
  if(@this == 1)
  {
    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);

    testRunning=0;
    step=0;

    write("==========================================");
    write("TEST STOPPED FROM CONTROL PANEL");
    write("==========================================");

    @sysvar::MasterCtrl::StopTest = 0;
  }
}


/* ============================================================
   PERIODIC TIMERS
   ============================================================ */

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


/* ============================================================
   FIVE DAY TEST

   START:
   OFF       2 SEC
   STANDBY   2 SEC

   EACH DAY:
   FLOAT
   ISOLATION OPEN 1 SEC
   ISOLATION CLOSE
   FLOAT 18 HOURS
   STANDBY 6 HOURS

   REPEAT 5 TIMES

   48V EPAS:
   MODE CHANGES NORMAL
   ISOLATION COMMAND IS SKIPPED
   ============================================================ */

on timer seqTimer
{
  if(!testRunning)
    return;


  /* STARTUP - STANDBY 2 SEC */

  if(step==0)
  {
    setMode(1);
    setIsolation(1);

    write("STARTUP - STANDBY - 2 SEC");

    step=1;
    setTimer(seqTimer,2000);
  }


  /* DAY 1 - FLOAT + ISO OPEN */

  else if(step==1)
  {
    setMode(3);
    setIsolation(0);

    write("DAY 1 - FLOAT - ISOLATION OPEN - 1 SEC");

    step=2;
    setTimer(seqTimer,1000);
  }

  else if(step==2)
  {
    setIsolation(1);

    write("DAY 1 - ISOLATION CLOSE - FLOAT 18 HOURS");

    step=3;
    setTimer(seqTimer,64800000);
  }

  else if(step==3)
  {
    setMode(1);
    setIsolation(1);

    write("DAY 1 - STANDBY - 6 HOURS");

    step=4;
    setTimer(seqTimer,21600000);
  }


  /* DAY 2 */

  else if(step==4)
  {
    setMode(3);
    setIsolation(0);

    write("DAY 2 - FLOAT - ISOLATION OPEN - 1 SEC");

    step=5;
    setTimer(seqTimer,1000);
  }

  else if(step==5)
  {
    setIsolation(1);

    write("DAY 2 - ISOLATION CLOSE - FLOAT 18 HOURS");

    step=6;
    setTimer(seqTimer,64800000);
  }

  else if(step==6)
  {
    setMode(1);
    setIsolation(1);

    write("DAY 2 - STANDBY - 6 HOURS");

    step=7;
    setTimer(seqTimer,21600000);
  }


  /* DAY 3 */

  else if(step==7)
  {
    setMode(3);
    setIsolation(0);

    write("DAY 3 - FLOAT - ISOLATION OPEN - 1 SEC");

    step=8;
    setTimer(seqTimer,1000);
  }

  else if(step==8)
  {
    setIsolation(1);

    write("DAY 3 - ISOLATION CLOSE - FLOAT 18 HOURS");

    step=9;
    setTimer(seqTimer,64800000);
  }

  else if(step==9)
  {
    setMode(1);
    setIsolation(1);

    write("DAY 3 - STANDBY - 6 HOURS");

    step=10;
    setTimer(seqTimer,21600000);
  }


  /* DAY 4 */

  else if(step==10)
  {
    setMode(3);
    setIsolation(0);

    write("DAY 4 - FLOAT - ISOLATION OPEN - 1 SEC");

    step=11;
    setTimer(seqTimer,1000);
  }

  else if(step==11)
  {
    setIsolation(1);

    write("DAY 4 - ISOLATION CLOSE - FLOAT 18 HOURS");

    step=12;
    setTimer(seqTimer,64800000);
  }

  else if(step==12)
  {
    setMode(1);
    setIsolation(1);

    write("DAY 4 - STANDBY - 6 HOURS");

    step=13;
    setTimer(seqTimer,21600000);
  }


  /* DAY 5 */

  else if(step==13)
  {
    setMode(3);
    setIsolation(0);

    write("DAY 5 - FLOAT - ISOLATION OPEN - 1 SEC");

    step=14;
    setTimer(seqTimer,1000);
  }

  else if(step==14)
  {
    setIsolation(1);

    write("DAY 5 - ISOLATION CLOSE - FLOAT 18 HOURS");

    step=15;
    setTimer(seqTimer,64800000);
  }

  else if(step==15)
  {
    setMode(1);
    setIsolation(1);

    write("DAY 5 - STANDBY - 6 HOURS");

    step=16;
    setTimer(seqTimer,21600000);
  }


  /* TEST COMPLETE */

  else if(step==16)
  {
    cancelTimer(t100);
    cancelTimer(t500);
    cancelTimer(t1000);
    cancelTimer(seqTimer);

    testRunning=0;

    write("==========================================");
    write("5 DAY TEST COMPLETE - 120 HOURS");
    write("==========================================");

    /*
       IMPORTANT:
       Do NOT call stop() here.

       Measurement stays running.
       This allows the Panel to remain available and avoids
       tying the test lifecycle to CANalyzer Measurement Stop.

       Logging stop will be integrated separately.
    */
  }
}
