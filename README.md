

variables
{
  int systemType = 0;
}

/* 1 = EBB
   2 = EMB
   3 = 48V
   4 = EPAS
*/

on start
{
  write("System selector loaded");
}

void selectSystem(int type)
{
  systemType = type;

  if (type == 1)
  {
    write("EBB selected");
  }
  else if (type == 2)
  {
    write("EMB selected");
  }
  else if (type == 3)
  {
    write("48V selected");
  }
  else if (type == 4)
  {
    write("EPAS selected");
  }
}