**Summary**

This document is an overview of Scrive Print to eSign Windows printer
infrastructure. Describing its repositories, dependencies and build
process.

Middleware server
=================

Hosts Windows "Scrive Print to eSign Printer driver“ Installer and
provides at least these services:

-   Webserver (Happstack 7.3.5) that accepts HTTP PUT request with
    attached PDF or PostScript data.
-   Does PostScript to PDF conversion and provides PDF tools for text
    extraction, anchoring, template matching
-   Authentication of Scrive user (OAuth)
-   Provides on-the-fly generation/slipstreaming of users OAuth
    (Persistent token) credentials by updating (7zip) and
    codesigning (ossl) of "Scrive Print to eSign Printer driver“
    Installer
-   Success and error pages

  ----------------- -- ----------------------------------------------------------------------------------------------------------
  Components:          /

                       

  Dependencies:        /
                       
                       OpenSSL signcode utility
                       
                       7z archiver

                       

  Build process:       TeamCity:Other Stuff CentOS 7.x / PhoneFamily Middleware Prerequisites: /
                       
                       Version: /
                       
                       Build command: Command Line
                       
                       Custom script: ./teamcity.sh

                       

  Deploy process:      /

                       

  Source:              [<https://github.com/scrive/phone-family-middleware>](https://github.com/scrive/phone-family-middleware)

                       

  Maintainer:          [<https://github.com/bugthunk>](https://github.com/bugthunk)
  ----------------- -- ----------------------------------------------------------------------------------------------------------

Installer
=========

Windows "Scrive Print to eSign Printer driver“ Installer unpacks its
content in windows temp folder and executes Scrive Setup
(ScriveSetup.exe) which:

-   Installs and configures: Scrive Port Monitor, Scrive Printer Port,
    Scrive Printer Driver, Scrive transporter tools (uploader,
    login, ..)
-   Authenticates User:OAuth credentials can be provided within
    installer in pdf995.ini fileIf older PDF995 printer is present
    pdf995.ini file is overrided with that oneIf credentials are missing
    "ScriveLogIn.exe“ is executed and user can enter his/her Scrive
    credentials as email/password values.OAuth(Personal token) values
    are then obtained from Scrive DB.
-   Opens "Devices and Printers“ panel where user can see "Scrive Print
    to eSign Printer“

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------
    ----------------- -- ----------------------------------------------------------------------------------------------------------------------------------------------
    Components:          Scrive Port Monitor ([RedMon -](http://pages.cs.wisc.edu/~ghost/redmon/)[Redirection Port Monitor](http://pages.cs.wisc.edu/~ghost/redmon/))
                         
                         Scrive Printer Driver (Microsoft PostScript driver v5)
                         
                         Scrive transport tools (look at “\[\#3. Transport tools|outline 3. Transport tools\]”)
                         
                         [7zip SFX module](https://sourceforge.net/projects/sevenzip/files/7-Zip/)

                         

    Dependencies:        OpenSSL signcode utility
                         
                         7z archiver

                         

    Build process:       TeamCity:Other Stuff CentOS 7.x / Scrive Printer Driver Prerequisites:
                         
                         Microsoft Authentication codesigning certificate
                         
                         Version: /
                         
                         Build command: Command Line
                         
                         Custom script: ./generate\_exe.sh

                         

    Deploy process:      / - Manual copy of artifacts to "\[\#1. Middleware server|outline 1. Middleware server\]“

                         

    Source:              [<https://github.com/scrive/scrive-printer-windows>](https://github.com/scrive/scrive-printer-windows)

                         

    Maintainer:          [<https://github.com/ernes32>](https://github.com/ernes32)
    ----------------- -- ----------------------------------------------------------------------------------------------------------------------------------------------

  -----------------------------------------------------------------------------------------------------------------------------------------------------------------------

Transport tools
===============

Set of tools for Windows "Scrive Print to eSign Printer driver“

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
    ----------------- -- ------------------------------------------------------------------------------------------------------------------------------------------------------------------
    Components:          Scrive Setup
                         
                         Scrive Upload
                         
                         Scrive LogIn

                         

    Dependencies:        Microsoft Visual Studio 2013Microsoft [WTL](https://en.wikipedia.org/wiki/Windows_Template_Library)/[ATL](https://en.wikipedia.org/wiki/Active_Template_Library)
                         
                         Microsoft Platform SDK

                         

    Build process:       TeamCity:
                         
                         Other Stuff Windows / Scrive PostScript Printer Driver Prerequisites:
                         
                         MSBuild v12 Toolset for .NET, Windows OS
                         
                         Version:ScriveLogIn.rc
                         
                         ScriveSetup.rc
                         
                         ScriveUpload.rc
                         
                         Build command:MSBuild
                         
                         Build file: Scrive.sln

                         

    Deploy process:      / - Manual copy of artifacts to "\[\#2. Installer|outline 2. Installer\]“

                         

    Source:              [<https://github.com/scrive/transporter>](https://github.com/scrive/transporter)

                         

    Maintainer:          [<https://github.com/ernes32>](https://github.com/ernes32)
    ----------------- -- ------------------------------------------------------------------------------------------------------------------------------------------------------------------

  -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------


