win10-autoactivate
===========

Script to read + install Windows 8+ OEM license key from a PC's firmware.

Description
-------------

PCs shipped with Windows 10 don't have any OEM key sticker, nor can they be activated by an OEM certificate and single OEM key anymore.
When imaging these PCs, Windows should automatically read the key from the BIOS and auto-activate, but in most cases it doesn't, especially when using an image rather than a basic install.

Read key from firmware(from ACPI -> MSDM table -> byte offset 56 to end) then install using slmgr.vbs.

Usage
-------------

Generate activate.exe from activate.py using PyInstaller.

`pyinstaller.py --onefile activate.py`

Place activate.exe inside your image, usually in C:\Drivers

Using Windows System Image Manager, create your unattend file.
* In amd64_Microsoft_Windows-Shell-Setup_neutral
  * FirstLogonCommands
    * SynchronousCommand (CommandLine: C:\Drivers\activate.exe)

sysprep your image, then on your first login to the imaged machine (as long as it's by an Administrator), your system will activate.

Requirements
-------------

-Windows 8 or higher (32 or 64 bit)  
-tested with Python 2.7
