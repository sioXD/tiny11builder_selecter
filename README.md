# tiny11builder

Scripts to build a trimmed-down Windows 11 image!
<br>
<br>
### Changes from the original tiny11builder

- added a menu where you can decide what you want to download
    - **Options**:
        - `1.` normal tiny11
        - `2.` tiny11 with edge
        - `3.` custom selection menu with **GUI** (you can select what you want to delete and what to keep)
        - `4.` tiny11 with edge and with windows key input field

<br>
<img src="./small_GUI.png" alt="GUI" width="300"/>
<br> 


<details>
<summary>code changes</summary>

### This is just a list of the code changes I made in the code  

- added a choice switchcase
- made most of the delete stuff into functions for better readability
- spit outlook from DevHome for better selection
- Added an GUI for choice 3: you select the thing you want to delete (`Load_reg` **must** always be selectet)
- added the option for the activation key to be given per input or hardcode    

</details> <br> <br> 

Since it is written in PowerShell, you need to set the execution policy to  `Unrestricted`, so that you could run the script.
If you haven't done this before, make sure to run `Set-ExecutionPolicy unrestricted` as administrator in PowerShell before running the script, otherwise it would just crash.


This is a script created to automate the build of a streamlined Windows 11 image, similar to tiny11.
My main goal is to use only Microsoft utilities like DISM, and no utilities from external sources. The only executable included is **oscdimg.exe**, which is provided in the Windows ADK and it is used to create bootable ISO images. 
Also included is an unattended answer file, which is used to bypass the Microsoft Account on OOBE and to deploy the image with the `/compact` flag.
It's open-source, **so feel free to add or remove anything you want!** Feedback is also much appreciated.

Also, for the very first time, **introducing tiny11 core builder**! A more powerful script, designed for a quick and dirty development testbed. Just the bare minimun, none of the fluff. 
This script generates a significantly reduced Windows 11 image. However, it's not suitable for regular use due to its lack of serviceability - you can't add languages, updates, or features post-creation. tiny11 Core is not a full Windows 11 substitute but a rapid testing or development tool, potentially useful for VM environments.

Instructions:

1. Download Windows 11 from the Microsoft website (<https://www.microsoft.com/software-download/windows11>)
2. Mount the downloaded ISO image using Windows Explorer.
3. Select the drive letter where the image is mounted (only the letter, no colon (:))
4. Select the SKU that you want the image to be based.
5. Sit back and relax :)
6. When the image is completed, you will see it in the folder where the script was extracted, with the name tiny11.iso

What is removed:

- Clipchamp
- News
- Weather
- Xbox (although Xbox Identity provider is still here, so it should be possible to be reinstalled with no issues)
- GetHelp
- GetStarted
- Office Hub
- Solitaire
- PeopleApp
- PowerAutomate
- ToDo
- Alarms
- Mail and Calendar
- Feedback Hub
- Maps
- Sound Recorder
- Your Phone
- Media Player
- QuickAssist
- Internet Explorer
- Tablet PC Math
- Edge
- OneDrive

For tiny11 core:
- all of the above +
- Windows Component Store (WinSxS)
- Windows Defender (only disabled, can be enabled back if needed)
- Windows Update (Windows Update wouldn't work anyway without WinSxS, so enabling it would only put the system in a state where it would try to update but fail spectacularily)
- WinRE
<br>
Keep in mind that **you cannot add back features in tiny11 core**!
</br>
<br>
You will be asked during image creation if you want to enable .net 3.5 support!
</br>
Known issues:

1. Although Edge is removed, there are some remnants in the Settings. But the app in itself is deleted. You can install any browser using WinGet (after you update the app using Microsoft Store). If you want Edge, Copilot and Web Search back, simply install Edge using Winget: `winget install edge`.
<br>
Note: You might have to update Winget before being able to install any apps, using Microsoft Store.
<br>
</br>
2. Outlook and Dev Home might reappear after some time.
<br>
</br>
3. If you are using this script on arm64, you might see a glimpse of an error while running the script. This is caused by the fact that the arm64 image doesn't have OneDriveSetup.exe included in the System32 folder.

Features to be implemented:
- ~~disabling telemetry~~ (Implemented in the 04-29-24 release!)
- more ad suppression
- improved language and arch detection
- more flexibility in what to keep and what to delete
- maybe a GUI???

And that's pretty much it for now!
Thanks for trying it and let me know how you like it!
