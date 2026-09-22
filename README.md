

# Navigate to your folder
cd "C:\12V and 48V A3 UCAP CAN Config\A3 UCAP All Modules Config\A3 UCAP All Modules Config"

# Target the state configuration file where the window signals actually live
$StateFile = "UCAP_All_Module_Config.stcfg"
$Text = [System.IO.File]::ReadAllText($StateFile)

Write-Host "Updating internal signal mapping paths inside the .stcfg file..." -ForegroundColor Cyan

# Force all the CAN1 window signal references over to their true channel assignments
$Text = $Text.Replace("CAN1::DCDCE", "CAN2::DCDCE")
$Text = $Text.Replace("CAN1::DCDCF", "CAN2::DCDCF")
$Text = $Text.Replace("CAN1::DCDCG", "CAN2::DCDCG")

# Save changes cleanly back to the state file
[System.IO.File]::WriteAllText($StateFile, $Text)

Write-Host "SUCCESS! The state layout paths are updated." -ForegroundColor Green
