

variables
{
  /* ============================
       48V EPAS - CAN5 / DBC5
     ============================ */

  message DBC5::BCM_AutoSar_Network_Mgmt       bcm;
  message DBC5::BodyInfo_3                     body;
  message DBC5::DCDCE_AutoSar_Network_Mgmt     dcdce;
  message DBC5::DCDCG_AutoSar_Network_Mgmt     dcdcg;
  message DBC5::EnergyMgmtBodyCtrl_3            ctrl;
  message DBC5::EnergyMgmtBodyInfo_3            info;

  msTimer timer100;
  msTimer timer500;
  msTimer timer1000;
  msTimer seqTimer;

  int step = 0;
}


/* ============================================================
   INITIALIZE 48V VALUES
   ============================================================ */

void init48V()
{
  /* ---------- BCM ---------- */

  bcm.BCM_AutoSarNMNodeId     = 129;
  bcm.BCM_AutoSarNMControl    = 0;
  bcm.BCM_AutoSarNMReserved1  = 255;
  bcm.BCM_AutoSarNMReserved2  = 255;
  bcm.BCM_GWOnBoardTester     = 255;
  bcm.BCM_GWNMProxy           = 255;
  bcm.BCM_AutoSarNMReserved3  = 255;
  bcm.BCM_AutoSarNMReserved4  = 255;


  /* ---------- BODY INFO ---------- */

  /*
     IMPORTANT:
     Your working 48V IG shows:
     Ignition_Status raw = 4 = RUN
  */

  body.DrStatTgate_B_Actl       = 0;
  body.FogLghtRearOn_B_Stat     = 0;
  body.Parklamp_Status          = 1;

  body.Ignition_Status          = 4;    // RUN

  body.TurnLghtLeft_D_Rq        = 0;
  body.BodySrvcRqd_B_Rq         = 0;
  body.Key_In_Ignition_Stat     = 0;
  body.Remote_Start_Status      = 0;
  body.Day_Night_Status         = 0;
  body.ValetMode_D_Mem          = 0;

  body.DimmingLvlEvnt_No_Actl   = 0;
  body.DrStatDrvErrCnt_B_Stat   = 0;
  body.Backlit_LED_Status       = 0;

  body.Dimming_Lvl              = 12;
  body.FuelPmpInhbt_B_Stat      = 0;
  body.CrashEvnt_D_Stat         = 3;
  body.TurnLghtRightOn_B_Stat   = 0;

  body.IgnKeyType_D_Actl        = 14;

  body.Litval                   = 0;
  body.DrStatRl_B_Actl          = 0;
  body.DrStatRr_B_Actl          = 0;
  body.LifeCycMde_D_Actl        = 0;
  body.TurnLghtLeftOn_B_Stat    = 0;
  body.PrkBrkActv_B_Actl        = 0;
  body.FogLghtFrontOn_B_Stat    = 0;
  body.Delay_Accy               = 0;
  body.DrStatInnrTgate_B_Actl   = 0;
  body.DrStatHood_B_Actl        = 0;
  body.DrStatPsngr_B_Actl       = 0;
  body.DrStatDrv_B_Actl         = 0;
  body.TurnLghtRight_D_Rq       = 0;


  /* ---------- DCDCE ---------- */

  dcdce.DCDCE_AutoSarNMControl   = 0;
  dcdce.DCDCE_AutoSarNMNodeId    = 129;
  dcdce.DCDCE_AutoSarNMReserved1 = 255;
  dcdce.DCDCE_AutoSarNMReserved2 = 255;
  dcdce.DCDCE_GWOnBoardTester    = 255;
  dcdce.DCDCE_GWNMProxy          = 255;
  dcdce.DCDCE_AutoSarNMReserved3 = 255;
  dcdce.DCDCE_AutoSarNMReserved4 = 255;


  /* ---------- DCDCG ---------- */

  dcdcg.DCDCG_AutoSarNMControl   = 0;
  dcdcg.DCDCG_AutoSarNMNodeId    = 129;
  dcdcg.DCDCG_AutoSarNMReserved1 = 255;
  dcdcg.DCDCG_AutoSarNMReserved2 = 255;
  dcdcg.DCDCG_GWOnBoardTester    = 255;
  dcdcg.DCDCG_GWNMProxy          = 255;
  dcdcg.DCDCG_AutoSarNMReserved3 = 255;
  dcdcg.DCDCG_AutoSarNMReserved4 = 255;


  /* ---------- 48V CONTROL ---------- */

  ctrl.UcmCplbtyTsnt_I_Rq       = 254;
  ctrl.UcmCplbtyFlyback_I_Rq    = 254;
  ctrl.UcmCplbtyStdySt_I_Rq     = 254;

  ctrl.UcmDistrPath_R_Calc       = 30;

  ctrl.UCapMduleMde_D_Rq         = 0;   // OFF

  ctrl.UCapMduleBst_U_Thres      = 0;
  ctrl.UCapMduleBck_U_Thres      = 0;


  /* ---------- 48V INFO ---------- */

  /*
     Latest working IG:
     Raw 8 = Physical 4.0
  */

  info.UcmAuxIn_I_MxAllw         = 8;

  info.UCapMduleChrg_I_Mx        = 254;
  info.UCapMduleDchrg_I_Mx       = 254;
}


/* ============================================================
   START
   ============================================================ */

on start
{
  init48V();

  /* Start OFF */
  ctrl.UCapMduleMde_D_Rq = 0;

  step = 0;

  /*
     Match your working IG periods:
     Ctrl + Info       = 100 ms
     BodyInfo          = 500 ms
     BCM/DCDCE/DCDCG   = 1000 ms
  */

  setTimer(timer100, 100);
  setTimer(timer500, 500);
  setTimer(timer1000, 1000);

  setTimer(seqTimer, 1000);

  write("48V CAN5 -> OFF");
}


/* ============================================================
   100 ms
   ============================================================ */

on timer timer100
{
  output(ctrl);
  output(info);

  setTimer(timer100, 100);
}


/* ============================================================
   500 ms
   ============================================================ */

on timer timer500
{
  output(body);

  setTimer(timer500, 500);
}


/* ============================================================
   1000 ms
   ============================================================ */

on timer timer1000
{
  output(bcm);
  output(dcdce);
  output(dcdcg);

  setTimer(timer1000, 1000);
}


/* ============================================================
   TEST SEQUENCE
   ============================================================ */

on timer seqTimer
{
  switch(step)
  {
    case 0:

      /* OFF -> STANDBY */
      ctrl.UCapMduleMde_D_Rq = 1;

      write("48V CAN5 -> STANDBY");

      step = 1;
      setTimer(seqTimer, 1000);
      break;


    case 1:

      /* STANDBY -> FLOAT */
      ctrl.UCapMduleMde_D_Rq = 3;

      write("48V CAN5 -> FLOAT");
      write("48V CAN5 -> HOLD FLOAT 90 SEC");

      step = 2;
      setTimer(seqTimer, 90000);
      break;


    case 2:

      /* FLOAT -> STANDBY */
      ctrl.UCapMduleMde_D_Rq = 1;

      write("48V CAN5 -> STANDBY");

      step = 3;
      setTimer(seqTimer, 1000);
      break;


    case 3:

      /* STANDBY -> OFF */
      ctrl.UCapMduleMde_D_Rq = 0;

      write("48V CAN5 -> OFF");

      step = 4;
      break;
  }
}