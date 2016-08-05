Transport tools
===============

Set of tools for Windows "Scrive Print to eSign Printer driver“

Components
----------

### Scrive Setup

After "Scrive Print to eSign Printer driver“ installer unpacks its
content in a windows temp folder Scrive Setup (ScriveSetup.exe) is
executed and does the following steps:

-   Check Windows OS version:If 64-bit version of OS is found
    “ScriveSetup64.exe“ binary is executed to install suitable version
    of printer driver components

-   Installs and configures: Scrive Port Monitor, Scrive Printer Port,
    Scrive Printer Driver, Scrive transporter tools (uploader,
    login, ..)

-   Authenticates User:
    OAuth credentials can be provided within installer in pdf995.ini file
    If older PDF995 printer is present pdf995.ini file is overrided with that one

    If credentials are missing Scrive LogIn("ScriveLogIn.exe“) is executed and user can enter
    his/her Scrive credentials as email/password values.
    OAuth(Personal token) values are then obtained from Scrive DB and stored in “pdf995.ini“ configuration file.
    
-   Opens "Devices and Printers“ panel where user can see "Scrive Print
    to eSign Printer“

### Scrive LogIn

Module used to authenticate with Scrive credentials(email/password)
against Scrive.com and fetches OAuth(Personal token) values which are
then stored in “pdf955.ini“ configuration file residnig on the same
location as Scrive LogIn("ScriveLogIn.exe“) module.

Successfuly obtained values will overwrite one stored in “pdf955.ini“
file.

### Scrive Upload

Module used to send files to “Scrive middleware server“ accepts a single
command line input argument as a path to an input file and does the
following when invoked:

-   Read input parameters from “pdf995.ini“
    [file:“ScriveURL](file:“ScriveURL)“ variable contains the URL of
    “Scrive middleware server““OAuth“ variables (OauthClientKey/Secret,
    OauthTokenKey/Secret ) contain a Scrive personal token credentialsIf
    OAuth credentials are missing Scrive LogIn("ScriveLogIn.exe“) is
    executed and user can enter his/her Scrive credentials as
    email/password values. OAuth(Personal token) values are then
    obtained from Scrive DB and stored in “pdf995.ini“ configuration
    file and the file has to be sent again.“Launch“ variable specifies
    the input file in case if no command line input argument
    is available. This is done for backward compatibility with older
    version of "Scrive Print to eSign Printer driver“ based on
    [PDF995](http://www.pdf995.com/) software stack.\
    “pdf995.ini“ configuration file should be on the same location as
    Scrive Upload ("ScriveUpload.exe“) module.
-   Send the input file to ScriveURL(“Scrive middleware server“):Read
    the input file to a data buffer.Generate “Authorization“ HTTP header
    from OAuth variables.Send the data over HTTP PUT request
    to ScriveURL.
-   Open the default web browser:If the file was successful sent read
    the “X-Open-Browser“ response header and open it in default
    web browser.

Dependencies:
-------------

Microsoft Visual Studio 2013

Microsoft
[WTL](https://en.wikipedia.org/wiki/Windows_Template_Library)/[ATL](https://en.wikipedia.org/wiki/Active_Template_Library)

Microsoft Platform SDK

Build process:
--------------

TeamCity Project:

Other Stuff Windows / Scrive PostScript Printer Driver Prerequisites:

MSBuild v12 Toolset for .NET, Windows OS

Version:ScriveLogIn.rc

ScriveSetup.rc

ScriveUpload.rc

Build command:MSBuild

Build file: Scrive.sln

Deploy process:
---------------

Manual copy of artifacts to "\[\#2. Installer|outline 2. Installer\]“

Maintainer:
-----------

[<https://github.com/ernes32>](https://github.com/ernes32)
