


# 1. Target your exact network folder path
cd "C:\12V and 48V A3 UCAP CAN Config\A3 UCAP All Modules Config\A3 UCAP All Modules Config"

# 2. Extract configuration text lines safely
\$File = "UCAP_All_Module_Config.cfg"
\(RawText = [System.IO.File]::ReadAllText(\)File)

Write-Host "Updating specific system paths for EBB, EPAS, and EMB..." -ForegroundColor Cyan

# 3. Apply the strict channel routing rules for all variations
# This cleanly shifts CAN1 over to CAN2 up to CAN6 for your duplicate windows
for (ch = 2; ch -le 6; \(ch++) {\)RawText = RawText.Replace("CAN1::DCDCE", "CANch`::DCDCE")
    \$RawText = RawText.Replace("CAN1::DCDCF", "CANch`::DCDCF")
    $RawText = $RawText.Replace("CAN1::DCDCG", "CAN$ch`::DCDCG")
}

# 4. Save the finalized configuration text block
[System.IO.File]::WriteAllText(File, RawText)

Write-Host "MASTER SUCCESS! All system maps are separated and saved." -ForegroundColor Green
