Nokia 5110 Simulator / Win95 OSR2 VMware 17 Player Instructions
===============================================================

This project is one of my first ever attempts at computer programming in Visual Basic 6 when I was about 16 years old. It accurately simulates the main GUI of a Nokia 5110 phone in a Windows environment. I never finished the project but it would have been interesting to get the Snake minigame :snake: running if anyone wants to continue work on it.

I realise the code is terrible in some places as it was my very first try at coding and it is very verbose. At the time I had no formal education or training as they didn't teach programming at school and I still didn't understand a lot of the fundamental concepts. Sorry :unamused:

The following instructions explain how to setup a Windows 95 Virtual Machine in VMware Workstation Player 17 and open the Visual Basic 6 project. If you want to take the less nostalgic route down memory lane it is still possible to successfully install Visual Basic 6 under modern versions of Windows and open the project from there.

Download and install VMWare17 from [here](https://drive.google.com/file/d/1GVdLzjO5dc3hCbM-NaRlvGvfGBRGX7-3/view?usp=sharing)

Install Windows 95 in VMware Player 
===================================

1. Create a New Virtual Machine
2. Select: "I will install the operating system later"
3. Name the virtual machine: Windows 95
4. Allocate the maximum disk size as 2GB
5. Select: "Store fdiskvirtual disk as a single file"
6. Download Dos6.21.img from https://www.allbootdisks.com/download/dos.html
7. Select: "Customize Hardware..."
8. Click the Add... button and select "Floppy Drive"
9. Select "Use floppy image file:" and browse to the Dos6.21.img file
10. Play the virtual machine
11. Enter the command: fdisk at prompt and select 1, 1, Y
12. Enter the command: format c:
13. Download Win95 OSR2 ISO from https://winworldpc.com/product/windows-95/osr-2
14. From the main menu select Player -> Removable Devices -> CD / DVD (IDE) 
15. In the settings dialog select "Use ISO image file:" and browse to the windows95b.iso file
16. Create a new folder in the c:\ drive using the command: mkdir c:\win95
17. Copy the setup files to the c:\ drive using the command: xcopy r:\ c:\win95 /s /e
18. Enter the command: c:\win95\setup.exe /IS
19. Search for an OEM CD-Key online. Google is your friend :wink:
20. Ignore the options to install the Network Adapter and Sound Card when prompted
21. From the main menu select Player -> Removable Devices -> Floppy -> Settings and select "Use physical drive:"
22. When Windows has finished installing click the prompt at the bottom of the screen to install VMware Tools
23. Install the SVGA drive manually by right clicking desktop -> Properties -> Settings tab -> Advanced Properties -> Change... -> Have Disk... and enter the path "C:\Program Files\VMware\VMware Tools\Drivers\video\" then browse for the file vmx_svga.drv
24. In Display Settings set your desired monitor resolution

Install Visual Studio 6.0
=========================

1. Download Visual Basic 6 ISO from https://winworldpc.com/product/microsoft-visual-bas/60
2. From the main menu select Player -> Removable Devices -> CD / DVD (IDE) 
3. In the settings dialog select "Use ISO image file:" and browse to the Visual Basic 6.0 Enterprise Edition.iso file
4. Open My Computer and double click on the CD-Drive
5. Install the application
6. Search for an OEM CD-Key online. Google is your friend :wink:
7. Choose to install Internet Explorer 4.01 SP1 without Windows Active Desktop Update

Installing Audio Drivers (Optional)
===================================

1. Shutdown the virtual machine safely in VMware Player
2. The current version of VMware has issues creating a VM with the necessary hardware to support audio. There is a solution:
   1. Open the file: C:\Users\<Your Username>\Documents\Virtual Machines\Windows 95\Windows 95.vmx in Notepad
   2. Change the hardware version configuration to virtualHW.version = "4"
   3. Delete any line starting with pciBridge or ending with pciSlotNumber
   4. Delete the following lines
     - gui.exitOnCLIHLT
     - hpet0.present
     - vmci0.present
     - vmci0.id
3. Start the virtual machine in VMware Player 
3. From the main menu select Player -> Removable Devices -> CD / DVD (IDE) 
4. In the settings dialog select "Use ISO image file:" and browse to the win95_drivers.iso file included this projects source code
5. Open the d:\ drive in My Computer and run the SBPCI128Setupus_w9x.exe file to install the audio drivers.
6. Click No when first asked to restart the computer and wait for the installer to complete
7. Restart the virtual machine and you should hear the familiar Windows startup sound

Connecting to the Internet (Optional)
=====================================

1. From the main menu select Player -> Removable Devices -> Network Adapter -> Settings -> "Bridged" and "Replicate physical network connection state"
2. Click Start -> Settings -> Control Panel
3. Open Network
4. Click Add...
5. Click Protocol then click Add...
6. Under Manufacturers tab choose Microsoft
7. Under Network Protocols, choose TCP/IP
8. Click OK and exit setup
9. Restart the virtual machine
10. Open Internet Explorer
11. Select "I want to set up a new connection using (LAN)" then "Connect using (LAN") and "No" to using a proxy server
12. Try navigating to www.google.com in Internet Explorer

Enabling USB Mass Storage Device Support (Optional)
===================================================

1. Shutdown the virtual machine safely in VMware Player
2. Select the virtual machine and from the main menu select Player -> Manage -> Virtual Machine Settings...
3. Click the Add... button and select "USB Controller"
4. Start the virtual machine in VMware Player
5. Cancel the Update Device Driver Wizard prompt on startup
6. Open Settings -> Control Panel -> System -> Device Manager
7. Remove all unknown "Other devices" from the list of hardware
8. From the main menu select Player -> Removable Devices -> CD / DVD (IDE) 
9. In the settings dialog select "Use ISO image file:" and browse to the win95_drivers.iso file included this projects source code
10. There is a bug in Windows when running the required XUSBSUPP.exe drivers file where it will run ScanDisk first but get stuck in an infinite loop. To overcome this:
    1. Open the c:\Windows folder in Explorer
    2. From the main menu select View -> Options -> View and uncheck Hide MS-DOS file extensions
    3. Rename Scandskw.exe to Scandskw.old
    4. Open the d:\Scandskw\Scandskw.vbp project in Visual Basic 6. Select File -> Make... Scandskw.exe and browse to the c:\Windows\System directory then compile
11. Open the d:\ drive in My Computer and run XUSBSUPP.exe this will install all the necessary USB Mass Storage drivers
12. Restart the virtual machine
13. Follow the Update Device Driver Wizard prompts to install the PCI Bridge and other drivers
14. Delete the c:\Windows\Scandskw.exe file created earlier and rename Scandskw.old with the exe extension
15. Insert the USB flash drive again and choose "Connect to a virtual machine" in the New USB Device Detected prompt
16. Follow the Update Device Driver Wizard prompts to install the Generic USB Mass Storage Class Device drivers
17. If you have followed the instructions correctly you should be able to see a Removable Disk (E:) in My Computer

Copying the project to the Virtual Machine
==========================================

Create an ISO image of the source code folder:

1. Download ImgBurn from https://www.imgburn.com/index.php?act=download
2. Open ImgBurn and select: "Create image file from files/folders"
3. Download ZIP of source code for this project from GitHub and extract to a folder
4. Browse to the source code folder in ImgBurn and select the output filename then write the ISO file
3. From the main menu of VMware player select Player -> Removable Devices -> CD / DVD (IDE) 
4. In the settings dialog select "Use ISO image file:" and browse to the ISO file
5. Create a folder named c:\repos\Nokia5110 and copy the source code to it
6. Open the Nokia5110.vpb project file in Visual Basic 6
7. Select Run -> Start to run the program

or...

Copy the source code to the host machine using a USB drive:

1. Download ZIP of source code for this project from GitHub and extract to a folder
2. Insert a USB flash drive and copy the code to it and remove the drive
3. Start the Windows 95 virtual machine created earlier
4. Insert the USB flash drive again and choose "Connect to the virtual machine" in the New USB Device Detected prompt
5. Open My Computer and you should be able to see a Removable Disk drive (E:)
6. Create a folder named c:\repos\Nokia5110 and copy the source code to it
7. Open the Nokia5110.vpb project file in Visual Basic 6
8. Select Run -> Start to run the program

Note
====

Unfortunately modern browsers flag some Visual Basic 6 executables as potential threats so you may need to use the the command line to download the release.

```
gh release download -R https://github.com/lschmid83/Nokia-5110 -A zip -O "c:\release\Nokia 5110.zip"
```
