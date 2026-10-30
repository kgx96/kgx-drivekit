<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="wordmark-light-text.png">
    <img alt="KGX DriveKit" src="wordmark-dark-text.png" width="420">
  </picture>
</p>

See what is filling your drives and free space safely. Folder sizes, the largest files, junk cleanup, moving folders to another drive, virus scans with Microsoft Defender, and finding the program that keeps a file "in use". Every risky step is explained and confirmed first.

**By KGX PRODUCTIONS**

---

## Download

From the [Releases](../../releases) page, get one of:

- **`KGXDriveKitSetup.exe`** (recommended): installs KGX DriveKit with its updater and uninstaller. The default folder is `C:\Program Files\KGXtools\KGX DriveKit`, or pick any folder.
- **`KGXDriveKit.exe`**: the program on its own, with nothing to install. Put it in any folder and run it.

**Requirements**

- Windows 10 or 11 (64-bit)
- Microsoft Edge WebView2 Runtime, which Windows 11 and an up-to-date Windows 10 already include. The program draws its own window with it. If it's missing, the program opens in a Microsoft Edge window instead.

Everything the tool keeps (settings, move history, update downloads) stays in its own folder, `…\KGXtools\KGX DriveKit\KGXDriveKit Data`. Nothing is written anywhere else on your PC.

### Setup

1. **Check**: shows the setup file's SHA-256. You can scan it with Microsoft Defender or look it up on [VirusTotal](https://www.virustotal.com/) (only the checksum is sent) before installing anything.
2. **Folder**: defaults to `C:\Program Files\KGXtools\KGX DriveKit`, which needs administrator rights (setup restarts as administrator and keeps the folder). There are quick picks for your other drives and your user folder, or browse to any folder.
3. **Review**: lists every file it will write, with its full path, size and SHA-256.
4. **Install**: each file is checked against its SHA-256 after copying.
5. **Done**: lists the installed files and shortcuts. **Start KGX DriveKit**, or **Open install folder**.

### Updating

Run **`updater.exe`** in the install folder, or **Help → Check for updates** in KGX DriveKit. It:
1. asks GitHub for the newest release of this repository
2. shows its notes
3. downloads `KGXDriveKitSetup.exe` and checks it against the SHA-256 GitHub lists for that file
4. closes KGX DriveKit
5. opens setup on its Review page for your install folder

Your settings and move history are kept.

### Uninstalling

Run **`uninstall.exe`** in the install folder, or **Help → Uninstall**. It lists everything it will delete and asks first:
- the program files
- every shortcut that opens something in the install folder
- the settings and move history
- itself

Other files in the folder are kept, and folders you moved with KGX DriveKit stay where they are. Setup writes no registry entries.

## What it does

| Tab | |
|---|---|
| **Drives** | Free and used space on every drive. Scan a whole drive or any folder. As administrator, whole NTFS drives use the [fast scan](#fast-scan). |
| **Explore** | Folder sizes, biggest first, with **Back** and **Up**. **Open**, **Scan**, **Move…** and **Delete…** on every row, plus a list of the largest files. Hover a name to see what it is. |
| **Cleanup** | Measures junk, then deletes what you tick. |
| **Move** | Moves your personal folders (Desktop, Documents, Downloads, Music, Pictures, Videos) to another drive the way Windows does it. Moves any other folder and leaves a link. History, with **Move back**. |
| **Security** | Microsoft Defender quick scan, full scan, scan one file or folder, update definitions. |
| **Processes** | Running programs with memory and CPU use. A **Live** toggle refreshes it every 2 seconds. **End tree…** stops a program and everything it started. |
| **Recycle Bin** | Size per drive, and Empty. |
| **Settings** | Every option, the color scheme (Dark, Light or Match Windows; Dev Library blue by default, plus Green, Teal, Purple and Amber), and a summary of the safety rules. |
| **Help** | How each part works, including how to get Windows off a full C:. |

### Fast scan

Run KGX DriveKit as administrator (**Restart as administrator**, top right) and scanning a whole NTFS drive reads the drive's file table (the MFT) in a few large reads instead of opening every folder. A full C: usually takes seconds instead of minutes, and nothing shows as **NO ACCESS**. It only reads; nothing on the drive is changed.

A folder that the last scan found with 20,000 files or more (**Scan** on its row in **Explore**) is read the same way. Smaller folders, a drive that isn't NTFS, or running without administrator rights use the normal folder-by-folder scan, which also reads several folders at once. Turn the fast scan off in **Settings → Scanning**.

### Progress

Scans, cleanup, deletes, moves and virus scans show a percentage bar, the time left and the elapsed time. Where stopping is safe there is a **Cancel** button.

### Warnings before anything is removed

Before a delete, move or cleanup, the program looks at what is inside and where it is:

- **Danger** needs you to type a word (DELETE, MOVE or CLEAN). Examples: installed programs, game saves, cloud-synced folders, Outlook mail files, password databases, crypto wallets, virtual machine disks.
- **Warning** needs a tick. Examples: large items (1 GB by default), files changed in the last 7 days, program data, Steam or a browser still open during cleanup.

### "The process cannot access the file because it is being used by another process"

When a delete or move fails because a file is open, the program asks Windows (Restart Manager) which programs hold it and lists them:

- **Show process** jumps to it in the Processes tab.
- **Force stop process tree and delete** ends it and the programs it started, then tries again. It asks first. Windows core processes and Microsoft Defender can never be ended from here.

### Cleanup covers

- **Windows:** your Temp folder and the Windows Temp folder (files older than 24 hours only), Windows Update downloads, Delivery Optimization cache, error reports, crash dumps
- **Graphics:** NVIDIA, AMD, Intel and DirectX shader caches
- **Steam:** shader cache, unfinished downloads, logs, dumps and web cache, in every Steam library
- **Browsers:** Chrome, Edge and Firefox caches (sign-ins, history and passwords are not touched)
- **Information only:** Windows.old, the hibernation file and your Downloads folder, with how to deal with each

Cleanup deletes permanently, like Windows Disk Cleanup. Files that are in use are skipped. Some Windows items need **Restart as administrator** (top right). The administrator copy closes the old window by itself.

### Moving folders safely

1. The folder is renamed first. Windows refuses this while a program has files open in it, so "in use" is caught before anything is copied.
2. Everything is copied, then checked: file count, sizes and, by default, every byte.
3. The link is created (or, for personal folders, Windows is told the new location).
4. Only then is the original removed.

If anything fails before step 4, the copy is deleted and the original is put back. Every move is listed in **Move → History** and can be moved back.

Steam games: use Steam's own **Settings → Storage → Move** instead.

### Moving Windows itself

Windows can't be moved to another drive while it is running, and no app can do that safely. **Help → Moving Windows** explains the options that do work: extending C: with free space on the same disk, cloning to a bigger drive, or a clean install on the other drive.

## Safety

- **Never deleted or moved:** drive roots, the Windows folder, Program Files, ProgramData, Users, your user folder or AppData itself, the Recycle Bin, System Volume Information, pagefile and hiberfil.
- **Links are never followed** (junctions, symlinks), so nothing is counted twice and cleanup never reaches outside a junk folder.
- **OneDrive online-only files** count as 0, because they use no space on your PC.
- Everything runs on your PC. The window is a local page on `127.0.0.1` with a random access token per launch. Nothing is sent anywhere. Virus scans use the Microsoft Defender already on your PC.

Note: the Windows folder looks bigger than it really is, because Windows stores some files once and links them from several places.

## Troubleshooting

| Problem | Fix |
|---|---|
| *Windows protected your PC* (SmartScreen) | The exe isn't code-signed. Click **More info → Run anyway**. |
| Antivirus flags the exe | A known false positive with unsigned programs. Download only from this repository's Releases, check the SHA-256 on [VirusTotal](https://www.virustotal.com/), and report false detections to [Microsoft](https://www.microsoft.com/en-us/wdsi/filesubmission). |
| Some folders show **NO ACCESS** | Use **Restart as administrator** and scan again. A whole-drive scan as administrator reads every folder. |
| A file is "in use" | Use **Show process** in the dialog, close that program, and try again. Or use **Force stop process tree and delete**. |
| Virus scan says Defender isn't available | Another antivirus is installed and has turned Defender off. Use that antivirus instead. |
| The window doesn't open | Install the [WebView2 Runtime](https://developer.microsoft.com/microsoft-edge/webview2/) (Evergreen), or start the program with `--edge-window` to use a Microsoft Edge window. From Command Prompt it also shows the local address to open in any browser. |

## License

Free to download and use. Source code is not published. See [LICENSE](LICENSE).

© KGX PRODUCTIONS 2026
