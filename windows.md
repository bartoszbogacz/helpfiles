# Windows

# Terminal

"defaults":
{
    "adjustIndistinguishableColors": "indexed",
    "bellStyle": "none",
    "colorScheme": "One Half Dark",
    "cursorShape": "vintage",
    "padding": "0",
    "scrollbarState": "hidden"
},


# PowerShell

While(1) {
    [void][System.Reflection.Assembly]::LoadWithPartialName('System.Windows.Forms')
    [System.Windows.Forms.SendKeys]::SendWait("{F15}")
    Start-Sleep -Seconds 90
}

$wsh = New-Object -ComObject WScript.Shell
while (1) {
  # Send Shift+F15 - this is the least intrusive key combination I can think of and is also used as default by:
  # http://www.zhornsoftware.co.uk/caffeine/
  # Unfortunately the above triggers a malware alert on Sophos so I needed to find a native solution - hence this script...
  $wsh.SendKeys('+{F15}')
  Start-Sleep -seconds 59
}

# VSCode

File -> Preferences -> Settings -> Search

files.autoSave: "onFocusChange"
editor.rulers: [90]
