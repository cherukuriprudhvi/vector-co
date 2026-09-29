
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

  int sys1 = 4;     // CAN1 = EPAS
  int sys2 = 4;     // CAN2 = EPAS
  int sys3 = 2;     // CAN3 = EMB
  int sys4 = 1;     // CAN4 = EBB
  int sys5 = 3;     // CAN5 = 48V EPAS
  int sys6 = 1;     // CAN6 = EBB

  msTimer t100;
  msTimer t500;
  msTimer t1000;
  msTimer seqTimer;

  int step = 0;


  /* ================= CAN 1 ================= */

  message DBC1::BCM_AutoSar_Network_Mgmt bcm1;
  message DBC1::BodyInfo_3 body1;

  message DBC1::DCDCE_AutoSar_Network_Mgmt dcdce1;
  message DBC1::DCDCF_AutoSar_Network_Mgmt dcdcf1;
  message DBC1::DCDCG_AutoSar_Network_Mgmt dcdcg1;

  message DBC1::EnergyMgmtBodyCtrl_1 ebbCtrl1;
  message DBC1::EnergyMgmtBodyInfo_1 ebbInfo1;

  message DBC1::EnergyMgmtBodyCtrl_2 embCtrl1;
  message DBC1::EnergyMgmtBodyInfo_2 embInfo1;

  message DBC1::EnergyMgmtBodyCtrl_3 v48Ctrl1;
  message DBC1::EnergyMgmtBodyInfo_3 v48Info1;

  message DBC1::EnergyMgmtBodyCtrl_4 epasCtrl1;
  message DBC1::EnergyMgmtBodyInfo_4 epasInfo1;


  /* ================= CAN 2 ================= */

  message DBC2::BCM_AutoSar_Network_Mgmt bcm2;
  message DBC2::BodyInfo_3 body2;

  message DBC2::DCDCE_AutoSar_Network_Mgmt dcdce2;
  message DBC2::DCDCF_AutoSar_Network_Mgmt dcdcf2;
  message DBC2::DCDCG_AutoSar_Network_Mgmt dcdcg2;

  message DBC2::EnergyMgmtBodyCtrl_1 ebbCtrl2;
  message DBC2::EnergyMgmtBodyInfo_1 ebbInfo2;

  message DBC2::EnergyMgmtBodyCtrl_2 embCtrl2;
  message DBC2::EnergyMgmtBodyInfo_2 embInfo2;

  message DBC2::EnergyMgmtBodyCtrl_3 v48Ctrl2;
  message DBC2::EnergyMgmtBodyInfo_3 v48Info2;

  message DBC2::EnergyMgmtBodyCtrl_4 epasCtrl2;
  message DBC2::EnergyMgmtBodyInfo_4 epasInfo2;


  /* ================= CAN 3 ================= */

  message DBC3::BCM_AutoSar_Network_Mgmt bcm3;
  message DBC3::BodyInfo_3 body3;

  message DBC3::DCDCE_AutoSar_Network_Mgmt dcdce3;
  message DBC3::DCDCF_AutoSar_Network_Mgmt dcdcf3;
  message DBC3::DCDCG_AutoSar_Network_Mgmt dcdcg3;

  message DBC3::EnergyMgmtBodyCtrl_1 ebbCtrl3;
  message DBC3::EnergyMgmtBodyInfo_1 ebbInfo3;

  message DBC3::EnergyMgmtBodyCtrl_2 embCtrl3;
  message DBC3::EnergyMgmtBodyInfo_2 embInfo3;

  message DBC3::EnergyMgmtBodyCtrl_3 v48Ctrl3;
  message DBC3::EnergyMgmtBodyInfo_3 v48Info3;

  message DBC3::EnergyMgmtBodyCtrl_4 epasCtrl3;
  message DBC3::EnergyMgmtBodyInfo_4 epasInfo3;


  /* ================= CAN 4 ================= */

  message DBC4::BCM_AutoSar_Network_Mgmt bcm4;
  message DBC4::BodyInfo_3 body4;

  message DBC4::DCDCE_AutoSar_Network_Mgmt dcdce4;
  message DBC4::DCDCF_AutoSar_Network_Mgmt dcdcf4;
  message DBC4::DCDCG_AutoSar_Network_Mgmt dcdcg4;

  message DBC4::EnergyMgmtBodyCtrl_1 ebbCtrl4;
  message DBC4::EnergyMgmtBodyInfo_1 ebbInfo4;

  message DBC4::EnergyMgmtBodyCtrl_2 embCtrl4;
  message DBC4::EnergyMgmtBodyInfo_2 embInfo4;

  message DBC4::EnergyMgmtBodyCtrl_3 v48Ctrl4;
  message DBC4::EnergyMgmtBodyInfo_3 v48Info4;

  message DBC4::EnergyMgmtBodyCtrl_4 epasCtrl4;
  message DBC4::EnergyMgmtBodyInfo_4 epasInfo4;


  /* ================= CAN 5 ================= */

  message DBC5::BCM_AutoSar_Network_Mgmt bcm5;
  message DBC5::BodyInfo_3 body5;

  message DBC5::DCDCE_AutoSar_Network_Mgmt dcdce5;
  message DBC5::DCDCF_AutoSar_Network_Mgmt dcdcf5;
  message DBC5::DCDCG_AutoSar_Network_Mgmt dcdcg5;

  message DBC5::EnergyMgmtBodyCtrl_1 ebbCtrl5;
  message DBC5::EnergyMgmtBodyInfo_1 ebbInfo5;

  message DBC5::EnergyMgmtBodyCtrl_2 embCtrl5;
  message DBC5::EnergyMgmtBodyInfo_2 embInfo5;

  message DBC5::EnergyMgmtBodyCtrl_3 v48Ctrl5;
  message DBC5::EnergyMgmtBodyInfo_3 v48Info5;

  message DBC5::EnergyMgmtBodyCtrl_4 epasCtrl5;
  message DBC5::EnergyMgmtBodyInfo_4 epasInfo5;


  /* ================= CAN 6 ================= */

  message DBC6::BCM_AutoSar_Network_Mgmt bcm6;
  message DBC6::BodyInfo_3 body6;

  message DBC6::DCDCE_AutoSar_Network_Mgmt dcdce6;
  message DBC6::DCDCF_AutoSar_Network_Mgmt dcdcf6;
  message DBC6::DCDCG_AutoSar_Network_Mgmt dcdcg6;

  message DBC6::EnergyMgmtBodyCtrl_1 ebbCtrl6;
  message DBC6::EnergyMgmtBodyInfo_1 ebbInfo6;

  message DBC6::EnergyMgmtBodyCtrl_2 embCtrl6;
  message DBC6::EnergyMgmtBodyInfo_2 embInfo6;

  message DBC6::EnergyMgmtBodyCtrl_3 v48Ctrl6;
  message DBC6::EnergyMgmtBodyInfo_3 v48Info6;

  message DBC6::EnergyMgmtBodyCtrl_4 epasCtrl6;
  message DBC6::EnergyMgmtBodyInfo_4 epasInfo6;
}


/* ============================================================
   INITIALIZE STATIC VALUES
   ============================================================ */

void initMessages()
{
  /* ---------- BCM ---------- */

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


  /* ---------- DCDCE ---------- */

  dcdce1.byte(0)=0; dcdce1.byte(1)=129;
  dcdce1.byte(2)=255; dcdce1.byte(3)=255;
  dcdce1.byte(4)=255; dcdce1.byte(5)=255;
  dcdce1.byte(6)=255; dcdce1.byte(7)=255;

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


  /* ---------- DCDCF ---------- */

  dcdcf1.byte(0)=0; dcdcf1.byte(1)=129;
  dcdcf1.byte(2)=255; dcdcf1.byte(3)=255;
  dcdcf1.byte(4)=255; dcdcf1.byte(5)=255;
  dcdcf1.byte(6)=255; dcdcf1.byte(7)=255;

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


  /* ---------- DCDCG ---------- */

  dcdcg1.byte(0)=0; dcdcg1.byte(1)=129;
  dcdcg1.byte(2)=255; dcdcg1.byte(3)=255;
  dcdcg1.byte(4)=255; dcdcg1.byte(5)=255;
  dcdcg1.byte(6)=255; dcdcg1.byte(7)=255;

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


  /* ---------- CTRL defaults ---------- */

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

  /* WORKING 48V CTRL */
  v48Ctrl1.byte(0)=254; v48Ctrl1.byte(1)=254;
  v48Ctrl1.byte(2)=254; v48Ctrl1.byte(3)=30;
  v48Ctrl1.byte(4)=0; v48Ctrl1.byte(5)=0;
  v48Ctrl1.byte(6)=0; v48Ctrl1.byte(7)=0;


  ebbCtrl2 = ebbCtrl1;
  ebbCtrl3 = ebbCtrl1;
  ebbCtrl4 = ebbCtrl1;
  ebbCtrl5 = ebbCtrl1;
  ebbCtrl6 = ebbCtrl1;

  embCtrl2 = embCtrl1;
  embCtrl3 = embCtrl1;
  embCtrl4 = embCtrl1;
  embCtrl5 = embCtrl1;
  embCtrl6 = embCtrl1;

  epasCtrl2 = epasCtrl1;
  epasCtrl3 = epasCtrl1;
  epasCtrl4 = epasCtrl1;
  epasCtrl5 = epasCtrl1;
  epasCtrl6 = epasCtrl1;

  v48Ctrl2 = v48Ctrl1;
  v48Ctrl3 = v48Ctrl1;
  v48Ctrl4 = v48Ctrl1;
  v48Ctrl5 = v48Ctrl1;
  v48Ctrl6 = v48Ctrl1;


  /* ---------- INFO defaults ---------- */

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


  /* ---------- WORKING 48V INFO ---------- */
  /* Aux raw 8 = physical 4.0 */

  v48Info1.byte(0)=8;
  v48Info1.byte(1)=254;
  v48Info1.byte(2)=254;
  v48Info1.byte(3)=0;
  v48Info1.byte(4)=0;
  v48Info1.byte(5)=0;
  v48Info1.byte(6)=0;
  v48Info1.byte(7)=0;


  ebbInfo2 = ebbInfo1;
  ebbInfo3 = ebbInfo1;
  ebbInfo4 = ebbInfo1;
  ebbInfo5 = ebbInfo1;
  ebbInfo6 = ebbInfo1;

  embInfo2 = embInfo1;
  embInfo3 = embInfo1;
  embInfo4 = embInfo1;
  embInfo5 = embInfo1;
  embInfo6 = embInfo1;

  epasInfo2 = epasInfo1;
  epasInfo3 = epasInfo1;
  epasInfo4 = epasInfo1;
  epasInfo5 = epasInfo1;
  epasInfo6 = epasInfo1;

  v48Info2 = v48Info1;
  v48Info3 = v48Info1;
  v48Info4 = v48Info1;
  v48Info5 = v48Info1;
  v48Info6 = v48Info1;


  /* =========================================================
     WORKING 48V BODY INFO
     ONLY applied to channels selected as sys = 3

     Ignition_Status = 4 = RUN
     ========================================================= */

  if(sys1==3)
  {
    body1.byte(0)=4;
    body1.byte(1)=0;
    body1.byte(2)=0;
    body1.byte(3)=12;
    body1.byte(4)=230;
    body1.byte(5)=0;
    body1.byte(6)=0;
    body1.byte(7)=0;
    body1.Ignition_Status=4;
  }

  if(sys2==3)
  {
    body2.byte(0)=4;
    body2.byte(1)=0;
    body2.byte(2)=0;
    body2.byte(3)=12;
    body2.byte(4)=230;
    body2.byte(5)=0;
    body2.byte(6)=0;
    body2.byte(7)=0;
    body2.Ignition_Status=4;
  }

  if(sys3==3)
  {
    body3.byte(0)=4;
    body3.byte(1)=0;
    body3.byte(2)=0;
    body3.byte(3)=12;
    body3.byte(4)=230;
    body3.byte(5)=0;
    body3.byte(6)=0;
    body3.byte(7)=0;
    body3.Ignition_Status=4;
  }

  if(sys4==3)
  {
    body4.byte(0)=4;
    body4.byte(1)=0;
    body4.byte(2)=0;
    body4.byte(3)=12;
    body4.byte(4)=230;
    body4.byte(5)=0;
    body4.byte(6)=0;
    body4.byte(7)=0;
    body4.Ignition_Status=4;
  }

  if(sys5==3)
  {
    body5.byte(0)=4;
    body5.byte(1)=0;
    body5.byte(2)=0;
    body5.byte(3)=12;
    body5.byte(4)=230;
    body5.byte(5)=0;
    body5.byte(6)=0;
    body5.byte(7)=0;
    body5.Ignition_Status=4;
  }

  if(sys6==3)
  {
    body6.byte(0)=4;
    body6.byte(1)=0;
    body6.byte(2)=0;
    body6.byte(3)=12;
    body6.byte(4)=230;
    body6.byte(5)=0;
    body6.byte(6)=0;
    body6.byte(7)=0;
    body6.Ignition_Status=4;
  }
}


/* ============================================================
   MODE
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
   ISOLATION
   0 = OPEN
   1 = CLOSE

   48V does NOTHING here
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
   100 ms
   CTRL + INFO
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
   500 ms BODY INFO
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
   1000 ms NETWORK MANAGEMENT
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


  /* =========================================================
     48V WORKING SETUP
     DCDCE + DCDCG
     ========================================================= */

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
   START
   ============================================================ */

on start
{
  initMessages();

  step=0;

  setMode(0);
  setIsolation(1);

  /* Transmit immediately */

  send100();
  send500();
  send1000();

  setTimer(t100,100);
  setTimer(t500,500);
  setTimer(t1000,1000);

  write("OFF - 1 SEC");

  setTimer(seqTimer,1000);
}


/* ============================================================
   PERIODIC TRANSMISSION
   ============================================================ */

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


/* ============================================================
   TEST SEQUENCE - ONE TIME

   OFF        1 SEC
   STANDBY    1 SEC
   FLOAT      1 SEC
   ISOL OPEN  1 SEC
   ISOL CLOSE 1 SEC
   FLOAT      2 MIN
   STANDBY    1 SEC
   OFF

   48V ignores isolation commands automatically.
   ============================================================ */

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
    /* Mode remains FLOAT.
       48V ignores this isolation command. */

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
    /* Mode remains FLOAT */

    write("FLOAT - 2 MIN");

    step=5;

    /* 120000 ms = 2 minutes */
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
