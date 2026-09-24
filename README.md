

variables
{
  int system1 = 0;
  int system2 = 0;
  int system3 = 0;
  int system4 = 0;
  int system5 = 0;
  int system6 = 0;
}


/* ================= CAN1 ================= */

on message CAN1.*
{
  if (system1 != 0) return;

  if (this.id == 273 || this.id == 304 ||
      this.id == 544 || this.id == 560 || this.id == 1024)
  {
    system1 = 1;
    write("CAN1 DETECTED: EBB");
  }
  else if (this.id == 272 || this.id == 305 ||
           this.id == 545 || this.id == 561 ||
           this.id == 769 || this.id == 1025)
  {
    system1 = 2;
    write("CAN1 DETECTED: EMB");
  }
  else if (this.id == 256 || this.id == 306 || this.id == 770)
  {
    system1 = 3;
    write("CAN1 DETECTED: 48V EPAS");
  }
  else if (this.id == 309 || this.id == 1026)
  {
    system1 = 4;
    write("CAN1 DETECTED: EPAS");
  }
}


/* ================= CAN2 ================= */

on message CAN2.*
{
  if (system2 != 0) return;

  if (this.id == 273 || this.id == 304 ||
      this.id == 544 || this.id == 560 || this.id == 1024)
  {
    system2 = 1;
    write("CAN2 DETECTED: EBB");
  }
  else if (this.id == 272 || this.id == 305 ||
           this.id == 545 || this.id == 561 ||
           this.id == 769 || this.id == 1025)
  {
    system2 = 2;
    write("CAN2 DETECTED: EMB");
  }
  else if (this.id == 256 || this.id == 306 || this.id == 770)
  {
    system2 = 3;
    write("CAN2 DETECTED: 48V EPAS");
  }
  else if (this.id == 309 || this.id == 1026)
  {
    system2 = 4;
    write("CAN2 DETECTED: EPAS");
  }
}


/* ================= CAN3 ================= */

on message CAN3.*
{
  if (system3 != 0) return;

  if (this.id == 273 || this.id == 304 ||
      this.id == 544 || this.id == 560 || this.id == 1024)
  {
    system3 = 1;
    write("CAN3 DETECTED: EBB");
  }
  else if (this.id == 272 || this.id == 305 ||
           this.id == 545 || this.id == 561 ||
           this.id == 769 || this.id == 1025)
  {
    system3 = 2;
    write("CAN3 DETECTED: EMB");
  }
  else if (this.id == 256 || this.id == 306 || this.id == 770)
  {
    system3 = 3;
    write("CAN3 DETECTED: 48V EPAS");
  }
  else if (this.id == 309 || this.id == 1026)
  {
    system3 = 4;
    write("CAN3 DETECTED: EPAS");
  }
}


/* ================= CAN4 ================= */

on message CAN4.*
{
  if (system4 != 0) return;

  if (this.id == 273 || this.id == 304 ||
      this.id == 544 || this.id == 560 || this.id == 1024)
  {
    system4 = 1;
    write("CAN4 DETECTED: EBB");
  }
  else if (this.id == 272 || this.id == 305 ||
           this.id == 545 || this.id == 561 ||
           this.id == 769 || this.id == 1025)
  {
    system4 = 2;
    write("CAN4 DETECTED: EMB");
  }
  else if (this.id == 256 || this.id == 306 || this.id == 770)
  {
    system4 = 3;
    write("CAN4 DETECTED: 48V EPAS");
  }
  else if (this.id == 309 || this.id == 1026)
  {
    system4 = 4;
    write("CAN4 DETECTED: EPAS");
  }
}


/* ================= CAN5 ================= */

on message CAN5.*
{
  if (system5 != 0) return;

  if (this.id == 273 || this.id == 304 ||
      this.id == 544 || this.id == 560 || this.id == 1024)
  {
    system5 = 1;
    write("CAN5 DETECTED: EBB");
  }
  else if (this.id == 272 || this.id == 305 ||
           this.id == 545 || this.id == 561 ||
           this.id == 769 || this.id == 1025)
  {
    system5 = 2;
    write("CAN5 DETECTED: EMB");
  }
  else if (this.id == 256 || this.id == 306 || this.id == 770)
  {
    system5 = 3;
    write("CAN5 DETECTED: 48V EPAS");
  }
  else if (this.id == 309 || this.id == 1026)
  {
    system5 = 4;
    write("CAN5 DETECTED: EPAS");
  }
}


/* ================= CAN6 ================= */

on message CAN6.*
{
  if (system6 != 0) return;

  if (this.id == 273 || this.id == 304 ||
      this.id == 544 || this.id == 560 || this.id == 1024)
  {
    system6 = 1;
    write("CAN6 DETECTED: EBB");
  }
  else if (this.id == 272 || this.id == 305 ||
           this.id == 545 || this.id == 561 ||
           this.id == 769 || this.id == 1025)
  {
    system6 = 2;
    write("CAN6 DETECTED: EMB");
  }
  else if (this.id == 256 || this.id == 306 || this.id == 770)
  {
    system6 = 3;
    write("CAN6 DETECTED: 48V EPAS");
  }
  else if (this.id == 309 || this.id == 1026)
  {
    system6 = 4;
    write("CAN6 DETECTED: EPAS");
  }
}