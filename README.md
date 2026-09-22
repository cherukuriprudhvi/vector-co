

# Set your exact working directory path from the image
cd "C:\12V and 48V A3 UCAP CAN Config\A3 UCAP All Modules Config\A3 UCAP All Modules Config"

# Target file
\$ConfigFile = "UCAP_All_Module_Config.cfg"

# Read the file contents cleanly
\(Content = [System.IO.File]::ReadAllText(\)ConfigFile)

Write-Host "Updating your graphics window tab names..." -ForegroundColor Cyan
\(Content =\)Content.Replace("CAN1_Graphics (2)", "CAN2_Graphics")
\(Content =\)Content.Replace("CAN1_Graphics (3)", "CAN3_Graphics")
\(Content =\)Content.Replace("CAN1_Graphics (4)", "CAN4_Graphics")
\(Content =\)Content.Replace("CAN1_Graphics (5)", "CAN5_Graphics")
\(Content =\)Content.Replace("CAN1_Graphics (6)", "CAN6_Graphics")

Write-Host "Updating database channels from DBC1 to matching CAN channels..." -ForegroundColor Cyan
# Replace the multi-line sequences cleanly for each isolated window block
\(Content =\)Content.Replace("CAN1`nDBC2", "CAN2`nDBC2")
\(Content =\)Content.Replace("CAN1`nDBC3", "CAN3`nDBC3")
\(Content =\)Content.Replace("CAN1`nDBC4", "CAN4`nDBC4")
\(Content =\)Content.Replace("CAN1`nDBC5", "CAN5`nDBC5")
\(Content =\)Content.Replace("CAN1`nDBC6", "CAN6`nDBC6")

# Save changes cleanly back to the configuration file structure
[System.IO.File]::WriteAllText(\(ConfigFile,\)Content)

Write-Host "Success! Your configuration file has been safely modified." -ForegroundColor Green
