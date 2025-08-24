# DPHXUnpackAndLoad
This tool's purpose is to help its users download, unpack, visualize and load MSFS soaring tasks that have been published on [WeSimGlide.org](https://wesimglide.org) using the [Discord Post Helper tool](https://github.com/siglr/DiscordPostHelper).

It consists of two applications. The main one being a Windows Forms application and the second one a small listening app that runs in the background in your system tray. Both are based on the Microsoft .NET Framework and as such, requires version 4.8 or later of that framework. You can download the .NET Framework here: https://dotnet.microsoft.com/en-us/download/dotnet-framework/thank-you/net48-web-installer.

To download the latest release from flightsim.to, click here: https://flightsim.to/file/62573/msfs-soaring-task-tools-dphx-unpack-load

To install for the first time, simply create a folder anywhere on your computer and extract the files in that folder. After first installation, the application supports auto-update so shouldn't be a problem anymore.

You should launch the tool at least once to adjust the settings and various folders. Double-check the MSFS folders that have been detected just in case they're wrong.

To associate .DPHX files to this application, simply double-click on one and Windows will ask you which program you want to use. Or, right-click on a file and select "Open with..." which should do the same. Then navigate to where you extracted the files and select the executable file "DPHX Unpack and Load.exe", then make sure to select "Always" so every .DPHX files you double-click next will automatically open in the tool.

For support and more information about the tool, you can visit the associated Discord Server using the links below.

There you will also find links to tutorial videos explaining how to use it.

Tutorial/Videos: https://discord.gg/ydRRJV9XUG

Questions/Support: https://discord.gg/DPnFBBqdaW

*Note: While some users report that Windows Defender is detecting threats from the main executable in this tool, they seem to be false positive as running analysis with BitDefender or Kasperky online returns zero threat at all. I've submitted the file to Microsoft Security Intelligence for an in-depth analysis and will report back with the final result, but the file right now shows "no malware detected".
You may need to exclude the folder where you extracted the files from your anti-virus software - see below!*

# Program flagged as potentially harmful by your anti-virus?
This is what is called a "false-positive". There is no virus or trojan in this tool, if you downloaded it from the official sources — what you're seeing is your anti-virus (like Microsoft Defender) machine-learning heuristic flagging your brand-new, unsigned EXE as “suspicious” because it’s never seen it before. The model is saying “I’ve never analyzed this binary; it looks like the kinds of packing/unpacking tools malware sometimes use, so I’ll quarantine it to be safe.”

## TL;DR
It's a **FALSE POSITIVE !**
**Fastest solution:** Exclude the entire folder where you extracted the files from the zip, then extract all the files again.

## Why it happens
1. **Unknown binary**
   Defender’s cloud-powered ML flags completely new executables that resemble packers, downloaders or unpackers (which many malware families use), especially when they’re not code-signed.

2. **Heuristic of “packer-style” behavior**
   If your app unpacks or loads other binaries at runtime (DPHX.Unpack & Load by name!), that looks eerily similar to malware droppers.

3. **No Authenticode signature**
   Unsigned executables carry no reputation in the Microsoft “SmartScreen” or Defender reputation systems, so they default to “untrusted.”

## What you and your users can do now
1. **Restore & Allow**
   * In the Windows Security prompt click **Actions → Restore**.
   * Then add an exclusion on either the file or your entire DPHX folder so Defender won’t re-quarantine.

2. **Submit for analysis**
   * Upload your EXE to Microsoft’s False-Positive portal:
     [https://www.microsoft.com/wdsi/filesubmission](https://www.microsoft.com/wdsi/filesubmission)
   * Microsoft will analyze it and, if benign, push an update so Defender stops flagging it.

## How to eliminate the warning long-term
1. **Code-sign your builds**
   * Purchase an Authenticode certificate and sign your installer and EXE.
   * Signed binaries build reputation in both SmartScreen and Defender’s reputation-based engine.

2. **Build a reputation**
   * Ship through an installer (MSI or setup-bootstrapper).
   * Host your download on a well-known domain (e.g. your official WeSimGlide.org) over HTTPS.
   * As more users install without incident, Defender’s reputation system will stop quarantining.

3. **Avoid suspicious packers**
   * If you’re using ILMerge, Costura.Fody, or any self-extracting stub, consider switching to a more “transparent” bundling method or separate DLLs.

4. **Automate submission**
   * Integrate the Windows Defender submission API into your CI pipeline so each build is auto-submitted for whitelisting.

## Bottom line:
This is a classic “false-positive” from Defender’s heuristic/ML engine. Code-signing your EXE and submitting it to Microsoft for analysis are the fastest routes to restore trust and stop these quarantines.

# Program doesn't start or reports a missing library?

Make sure you check out and do this first: https://discord.com/channels/1022705603489042472/1101255857683042466/1395158850104987688

1. Download both versions of the VC++ 2015–2022 redistributable:
:link: https://aka.ms/vs/17/release/vc_redist.x64.exe
:link: https://aka.ms/vs/17/release/vc_redist.x86.exe

2. Install both of them by running each of them.
**Why both?** Even though the app is x64 running on a Windows x64, some CefSharp dependencies are compiled for x86, and Windows will need both sets of runtimes available in parallel.

3. Reboot your computer

4. Try to launch the app again.

## VirusTotal
You can have [VirusTotal](https://www.virustotal.com/) analyze the files that are being detected by your anti-virus and see which other engines may also detect them to give you a better idea.
