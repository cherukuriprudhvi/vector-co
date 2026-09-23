

variables
{
  int detectedSystem = 0;
  // 0 = Unknown
  // 1 = EBB
  // 2 = EMB
  // 3 = 48V EPAS
  // 4 = EPAS
}

on message CAN1.*
{
  // EBB unique RX IDs
  if (this.id == 273 ||
      this.id == 304 ||
      this.id == 544 ||
      this.id == 560 ||
      this.id == 1024)
  {
    if (detectedSystem != 1)
    {
      detectedSystem = 1;
      write("CAN1 DETECTED: EBB");
    }
  }

  // EMB unique RX IDs
  else if (this.id == 272 ||
           this.id == 305 ||
           this.id == 545 ||
           this.id == 561 ||
           this.id == 769 ||
           this.id == 1025)
  {
    if (detectedSystem != 2)
    {
      detectedSystem = 2;
      write("CAN1 DETECTED: EMB");
    }
  }

  // 48V EPAS unique RX IDs
  else if (this.id == 256 ||
           this.id == 306 ||
           this.id == 770)
  {
    if (detectedSystem != 3)
    {
      detectedSystem = 3;
      write("CAN1 DETECTED: 48V EPAS");
    }
  }

  // EPAS unique RX IDs
  else if (this.id == 309 ||
           this.id == 1026)
  {
    if (detectedSystem != 4)
    {
      detectedSystem = 4;
      write("CAN1 DETECTED: EPAS");
    }
  }
}