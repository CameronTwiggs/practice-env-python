https://github.com/usebruno/bruno/releases/download/v2.12.0/bruno_2.12.0_x64_win.zip
param(
    [Parameter(Position=0)][string]$Arg,
    [switch]$ToClipboard
)

$map = @{
    "1" = "$PSScriptRoot\clip_1.txt"
    "2" = "$PSScriptRoot\clip_2.txt"
    "3" = "$PSScriptRoot\clip_3.txt"
}

if ($map.ContainsKey($Arg)) {
    $File = $map[$Arg]
} elseif ($Arg) {
    $File = $Arg
} else {
    $File = "$PSScriptRoot\clipboard_output.txt"
}

if ($ToClipboard) {
    $content = Get-Content -Path $File -Raw
    Set-Clipboard -Value $content
    Write-Host "Loaded $File into clipboard."
} else {
    $content = Get-Clipboard
    Set-Content -Path $File -Value $content -Force
    Write-Host "Saved clipboard to $File."
}
