

# Navigate directly to your directory path
cd "C:\12V and 48V A3 UCAP CAN Config\A3 UCAP All Modules Config\A3 UCAP All Modules Config"

# Define the target configuration file path
$File = "UCAP_All_Module_Config.cfg"
$RawText = [System.IO.File]::ReadAllText($File)

Write-Host "Updating specific system paths for EBB, EPAS, and EMB..." -ForegroundColor Cyan

# Replace the internal double-colon signal structures for tabs 2 through 6
$RawText = $RawText.Replace("CAN1::DCDCE", "CAN2::DCDCE")
$RawText = $RawText.Replace("CAN1::DCDCF", "CAN2::DCDCF")
$RawText = $RawText.Replace("CAN1::DCDCG", "CAN2::DCDCG")

# Save the modifications directly back to your file structure
[System.IO.File]::WriteAllText($File, $RawText)

Write-Host "SUCCESS! Your internal signal paths are re-routed to Channel 2." -ForegroundColor Green
