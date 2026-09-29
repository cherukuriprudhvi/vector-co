

variables
{
  /* ================= EMB - CAN3 / DBC3 ================= */

  message DBC3::BCM_AutoSar_Network_Mgmt       bcm;
  message DBC3::BodyInfo_3                     body;
  message DBC3::DCDCE_AutoSar_Network_Mgmt     dcdce;
  message DBC3::DCDCF_AutoSar_Network_Mgmt     dcdcf;
  message DBC3::EnergyMgmtBodyCtrl_2            ctrl;
  message DBC3::EnergyMgmtBodyInfo_2            info;

  msTimer timer100;
  msTimer timer500;
  msTimer timer1000;
  msTimer seqTimer;

  int step = 0;
}


/* =========================================================
   SET EXACT EMB VALUES FROM YOUR IG
   ========================================================= */

void initEMB()
{
  /* BCM */
  bcm.BCM_AutoSarNMNodeId     = 129;
  bcm.BCM_AutoSarNMControl    = 0;
  bcm.BCM_AutoSarNMReserved1  = 255;
  bcm.BCM_AutoSarNMReserved2  = 255;
  bcm.BCM_GWOnBoardTester     = 255;
  bcm.BCM_GWNMProxy           = 255;
  bcm.BCM_AutoSarNMReserved3  = 255;
  bcm.BCM_AutoSarNMReserved4  = 255;


  /* DCDCE */
  dcdce.DCDCE_AutoSarNMControl   = 0;
  dcdce.DCDCE_AutoSarNMNodeId    = 129;
  dcdce.DCDCE_AutoSarNMReserved1 = 255;
  dcdce.DCDCE_AutoSarNMReserved2 = 255;
  dcdce.DCDCE_GWOnBoardTester    = 255;
  dcdce.DCDCE_GWNMProxy          = 255;
  dcdce.DCDCE_AutoSarNMReserved3 = 255;
  dcdce.DCDCE_AutoSarNMReserved4 = 255;


  /* DCDCF */
  dcdcf.DCDCF_AutoSarNMControl   = 0;
  dcdcf.DCDCF_AutoSarNMNodeId    = 129;
  dcdcf.DCDCF_AutoSarNMReserved1 = 255;
  dcdcf.DCDCF_AutoSarNMReserved2 = 255;
  dcdcf.DCDCF_GWOnBoardTester    = 255;
  dcdcf.DCDCF_GWNMProxy          = 255;
  dcdcf.DCDCF_AutoSarNMReserved3 = 255;
  dcdcf.DCDCF_AutoSarNMReserved4 = 255;


  /* EMB CONTROL */
  ctrl.EMduleDistrPath_R_Calc2   = 30;
  ctrl.EMduleMde_D_Rq2           = 0;     // OFF
  ctrl.IsolSwtchOpen_U_Thres2    = 40;
  ctrl.IsolSwtch_B_Cmd2          = 1;     // CLOSE

  ctrl.DcdcOutULo_U_HystThres2   = 0;
  ctrl.DcdcAout_U_Rq2            = 13;
  ctrl.DcdcOutUHi_U_HystThres2   = 0;
  ctrl.PwBus_U_Rq2               = 13;
  ctrl.EMduleHystMx_U_Allw2      = 0;
  ctrl.EMduleHystMn_U_Allw2      = 6;


  /* EMB INFO */
  info.EMduleRgen_I_Actl2        = 0;
  info.EMduleBst_I_Actl2         = 0;
  info.EMduleRgen_IRate_Rsrv2    = 0;
  info.DcdcOutULo1_IRate_Actl2   = 0;
  info.EMduleBst_IRate_Rsrv2     = 0;
  info.DcdcOutULo2_IRate_Actl2   = 0;
  info.DcdcOutUHi2_IRate_Actl2   = 0;
  info.DcdcOutUHi1_IRate_Actl2   = 0;
  info.EMduleChrg_I_Mx2          = 20;
  info.EMduleDchrg_I_Mx2         = 20;
}


/* =========================================================
   START
   ========================================================= */

on start
{
  initEMB();

  ctrl.EMduleMde_D_Rq2  = 0;
  ctrl.IsolSwtch_B_Cmd2 = 1;

  step = 0;

  setTimer(timer100,100);
  setTimer(timer500,500);
  setTimer(timer1000,1000);

  /* OFF for 1 second */
  setTimer(seqTimer,1000);

  write("EMB TEST START -> OFF");
}


/* =========================================================
   ORIGINAL IG MESSAGE PERIODS
   ========================================================= */

/* Ctrl + Info = 100 ms */
on timer timer100
{
  output(ctrl);
  output(info);

  setTimer(timer100,100);
}


/* BodyInfo = 500 ms */
on timer timer500
{
  output(body);

  setTimer(timer500,500);
}


/* BCM + DCDCE + DCDCF = 1000 ms */
on timer timer1000
{
  output(bcm);
  output(dcdce);
  output(dcdcf);

  setTimer(timer1000,1000);
}


/* =========================================================
   TEST SEQUENCE
   ========================================================= */

on timer seqTimer
{
  switch(step)
  {
    case 0:

      /* OFF finished -> STANDBY */
      ctrl.EMduleMde_D_Rq2 = 1;
      ctrl.IsolSwtch_B_Cmd2 = 1;

      write("EMB -> STANDBY");

      step = 1;
      setTimer(seqTimer,1000);
      break;


    case 1:

      /* STANDBY -> FLOAT */
      ctrl.EMduleMde_D_Rq2 = 3;
      ctrl.IsolSwtch_B_Cmd2 = 1;

      write("EMB -> FLOAT");

      step = 2;
      setTimer(seqTimer,1000);
      break;


    case 2:

      /* FLOAT 1 sec -> isolation OPEN */
      ctrl.IsolSwtch_B_Cmd2 = 0;

      write("EMB -> ISOLATION OPEN");

      step = 3;
      setTimer(seqTimer,1000);
      break;


    case 3:

      /* CLOSE isolation */
      ctrl.IsolSwtch_B_Cmd2 = 1;

      write("EMB -> ISOLATION CLOSE");
      write("EMB -> FLOAT HOLD 90 SEC");

      step = 4;
      setTimer(seqTimer,90000);
      break;


    case 4:

      /* After 90 sec FLOAT -> STANDBY */
      ctrl.EMduleMde_D_Rq2 = 1;
      ctrl.IsolSwtch_B_Cmd2 = 1;

      write("EMB -> STANDBY");

      step = 5;
      setTimer(seqTimer,1000);
      break;


    case 5:

      /* STANDBY -> OFF */
      ctrl.EMduleMde_D_Rq2 = 0;
      ctrl.IsolSwtch_B_Cmd2 = 1;

      write("EMB -> OFF");

      step = 6;
      break;
  }
}