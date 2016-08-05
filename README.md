Transport tools
===============

Set of tools for Windows "Scrive Print to eSign Printer“

|  |  | Description |
|-----------------|---|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [Components](#Components): |  | [Scrive Setup](#Setup), [Scrive Upload](#Upload), [Scrive LogIn](#LogIn) |
|  |  |  |
| [Dependencies](#Dependencies): |  | Microsoft Visual Studio 2013, Microsoft [WTL](https://en.wikipedia.org/wiki/Windows_Template_Library)/[ATL](https://en.wikipedia.org/wiki/Active_Template_Library), Microsoft Platform SDK |
|  |  |  |
| Build process: |  | TeamCity project: Other Stuff Windows/Scrive PostScript Printer Driver <br>Prerequisites: MSBuild v12 Toolset for .NET, Windows OS <br>Version: [ScriveLogIn.rc](https://github.com/scrive/transporter/blob/master/login/ScriveUpload.rc) [ScriveSetup.rc](https://github.com/scrive/transporter/blob/master/setup/ScriveSetup.rc) [ScriveUpload.rc](https://github.com/scrive/transporter/blob/master/uploader/ScriveUpload.rc) <br>Build command: MSBuild <br>Build file: [scrive.sln](https://github.com/scrive/transporter/blob/master/scrive.sln) |
|  |  |  |
| [Deploy process:](#Deploy) |  | Manual copy of artifacts to [scrive-printer-windows](https://github.com/scrive/scrive-printer-windows) |
|  |  |  |
| Source: |  | [<https://github.com/scrive/transporter>](https://github.com/scrive/transporter) |
|  |  |  |
| Maintainer : |  | [<https://github.com/ernes32>](https://github.com/ernes32) |


Components<a name="Components"></a>
----------

### Scrive Setup<a name="Setup"></a>

After "Scrive Print to eSign Printer driver“ installer unpacks its
content in a windows temp folder Scrive Setup (ScriveSetup.exe) is
executed and does the following steps:

-   Check Windows OS version:

    If 64-bit version of OS is found “ScriveSetup64.exe“ binary is executed to install suitable version
    of printer driver components

-   Installs and configures:

    Scrive Port Monitor, Scrive Printer Port, Scrive Printer Driver, Scrive transporter tools (uploader,login, ..)

-   Authenticates User:

    OAuth credentials can be provided within installer in pdf995.ini file

    If older PDF995 printer is present pdf995.ini file is overrided with that one

    If credentials are missing Scrive LogIn("ScriveLogIn.exe“) is executed and user can enter
    his/her Scrive credentials as email/password values.
    OAuth(Personal token) values are then obtained from Scrive DB and stored in “pdf995.ini“ configuration file.
    
-   Opens "Devices and Printers“ panel where user can see "Scrive Print to eSign Printer“

### Scrive LogIn<a name="LogIn"></a>

Module used to authenticate with Scrive credentials(email/password) against Scrive.com and fetches OAuth(Personal token) values which are
then stored in “pdf955.ini“ configuration file residnig on the same location as Scrive LogIn("ScriveLogIn.exe“) module.

Successfuly obtained values will overwrite one stored in “pdf955.ini“ file.

### Scrive Upload<a name="Upload"></a>

Module used to send files to “Scrive middleware server“ accepts a single
command line input argument as a path to an input file and does the
following when invoked:

-   Read input parameters from “pdf995.ini“ file:
    
    “ScriveURL“ variable contains the URL of “Scrive middleware server“

    “OAuth“ variables (OauthClientKey/Secret, OauthTokenKey/Secret ) 
    contain a Scrive personal token credentials
    
    If OAuth credentials are missing Scrive LogIn("ScriveLogIn.exe“) is executed and user can enter his/her Scrive credentials as
    email/password values. OAuth(Personal token) values are then obtained from Scrive DB and stored in “pdf995.ini“ configuration
    file and the file has to be sent again.
    
    “Launch“ variable specifies the input file in case if no command line input argument is available. 
    This is done for backward compatibility with older version of "Scrive Print to eSign Printer driver“ based on
    [PDF995](http://www.pdf995.com/) software stack.
    
    “pdf995.ini“ configuration file should be on the same location as Scrive Upload ("ScriveUpload.exe“) module.
    
-   Send the input file to ScriveURL(“Scrive middleware server“):

    Read the input file to a data buffer.
    Generate “Authorization“ HTTP header from OAuth variables.
    Send the data over HTTP PUT request to ScriveURL.
    
-   Open the default web browser:

    If the file was successful sent read the “X-Open-Browser“ response header and open it in default
    web browser.

Dependencies:<a name="Dependencies"></a>
-------------

Microsoft Visual Studio 2013

Microsoft
[WTL](https://en.wikipedia.org/wiki/Windows_Template_Library)/[ATL](https://en.wikipedia.org/wiki/Active_Template_Library)

Microsoft Platform SDK

Build process:<a name="Build"></a>
--------------

TeamCity Project: Other Stuff Windows / Scrive PostScript Printer Driver 

Prerequisites: MSBuild v12 Toolset for .NET , Windows OS

Version:<a name="Version"></a>
[ScriveLogIn.rc](https://github.com/scrive/transporter/blob/master/login/ScriveUpload.rc)
[ScriveSetup.rc](https://github.com/scrive/transporter/blob/master/setup/ScriveSetup.rc)
[ScriveUpload.rc](https://github.com/scrive/transporter/blob/master/uploader/ScriveUpload.rc)

Build command: MSBuild

Build file: [scrive.sln](https://github.com/scrive/transporter/blob/master/scrive.sln)

Deploy process:<a name="Deploy"></a>
---------------

Manual copy of artifacts to [scrive-printer-windows](https://github.com/scrive/scrive-printer-windows)

Maintainer:
-----------

[<https://github.com/ernes32>](https://github.com/ernes32)
<br><br><br>
