

variables
{
  int detectedSystem = 0;

  message DBC1::EnergyMgmtBodyCtrl_1 ebbMsg;
  message DBC1::EnergyMgmtBodyCtrl_2 embMsg;
  message DBC1::EnergyMgmtBodyCtrl_3 v48Msg;
  message DBC1::EnergyMgmtBodyCtrl_4 epasMsg;
}

on message CAN1.*
{
  if (detectedSystem != 0)
    return;

  // EBB
  if (this.id == 273 ||
      this.id == 304 ||
      this.id == 544 ||
      this.id == 560 ||
      this.id == 1024)
  {
    detectedSystem = 1;

    ebbMsg.EMduleMde_D_Rq = 0;
    output(ebbMsg);

    write("CAN1 DETECTED: EBB");
    write("CAN1 EBB: OFF SENT");
  }

  // EMB
  else if (this.id == 272 ||
           this.id == 305 ||
           this.id == 545 ||
           this.id == 561 ||
           this.id == 769 ||
           this.id == 1025)
  {
    detectedSystem = 2;

    embMsg.EMduleMde_D_Rq2 = 0;
    output(embMsg);

    write("CAN1 DETECTED: EMB");
    write("CAN1 EMB: OFF SENT");
  }

  // 48V EPAS
  else if (this.id == 256 ||
           this.id == 306 ||
           this.id == 770)
  {
    detectedSystem = 3;

    v48Msg.UCapMduleMde_D_Rq = 0;
    output(v48Msg);

    write("CAN1 DETECTED: 48V EPAS");
    write("CAN1 48V EPAS: OFF SENT");
  }

  // EPAS
  else if (this.id == 309 ||
           this.id == 1026)
  {
    detectedSystem = 4;

    epasMsg.EMduleMde_D_Rq3 = 0;
    output(epasMsg);

    write("CAN1 DETECTED: EPAS");
    write("CAN1 EPAS: OFF SENT");
  }
}