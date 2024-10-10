
When starting PowerShell, users may encounter the following warning:
```
Re enable Import Module Psreadline warning⚠️
```
This script helps to resolve that issue. ✅

## Solution: 💡

Use the provided PowerShell script to change the encoding settings and prevent the warning from appearing.

### How to use the script: 📜

1. Clone the repository:
   ```bash
   git clone https://github.com/shivraj-prajapati/powershell-psreadline-warning.git
   ```

2. Run the script in PowerShell:
   ```powershell
   .\fix-psreadline-warning.ps1
   ```
If the script does not execute properly, you can copy and paste the following code directly into PowerShell:
```powershell
(Add-Type -PassThru -Name ScreenReaderUtil -Namespace WinApiHelper -MemberDefinition @'
  const int SPIF_SENDCHANGE = 0x0002;
  const int SPI_SETSCREENREADER = 0x0047;

  [DllImport("user32", SetLastError = true, CharSet = CharSet.Unicode)]
  private static extern bool SystemParametersInfo(uint uiAction, uint uiParam, IntPtr pvParam, uint fWinIni);

  public static void EnableScreenReader(bool enable)
  {
    var ok = SystemParametersInfo(SPI_SETSCREENREADER, enable ? 1u : 0u, IntPtr.Zero, SPIF_SENDCHANGE);
    if (!ok)
    {
      throw new System.ComponentModel.Win32Exception(Marshal.GetLastWin32Error());
    }
  }
'@)::EnableScreenReader($false);
```


