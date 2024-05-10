# Windows-Startup
Customizable Windows startup script

<#======================================================================================
         File Name : Startup.ps1
   Original Author : Kenneth C. Mazie
                   :
       Description : This is a Windows start-up script with pop-up notification and checks to
                   : assure things are not executed if already running or set.  It can be run 
                   : as a personal start-up script or as a domain start-up (with some editing).  
                   : It is intended to be executed from the Start Menu "All Programs\Startup" folder.
                   :
                   : The script will Start programs, map shares, set routes, and can email the results
                   : if desired.  The email subroutine is commented out.  You'll need to edit it yourself.
                   : When run with the "debug" variable set to TRUE it also displays status in the 
                   : PowerShell command window. Other wise all operation statuses are displayed in pop-up
                   : balloons near the system tray.
                   :
                   : To call the script use the following in a shortcut or in the RUN registry key.
                   : "C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -WindowStyle Hidden –Noninteractive -NoLogo -Command "&{C:\Startup.ps1}"
                   : Change the script name and path as needed to suit your environment.
                   :
                   : Be sure to edit all sections to suit your needs before executing.  Be sure to 
                   : enable sections you wish to run by un-commenting them at the bottom of the script.
                   :
                   : Route setting is done as a function of selecting a specific Network Adapter with the intent
                   : of manually altering your routes for hardline or WiFi connectivity.  This section you will
                   : need to customize to suit your needs or leave commented out.  This allowed me to
                   : alter the routing for my office (Wifi) or lab (hardline) by detecting whether my
                   : laptop was docked or not.  The hardline is ALWAYS favored as written.
                   :
                   : To identify process names to use run "get-process" by itself to list process 
                   : names that PowerShell will be happy with, just make sure each app you want to 
                   : identify a process name for is already running first.
                   :
                   : A 2 second sleep delay is added to smooth out processing but can be removed if needed.
                   :
             Notes : Sample script is safe to run as written, it will only load task manager and Firefox.
                   : All notification options are enabled.  For silent operation change them to $FALSE.
                   : Many commands are one-liner style, sorry if that causes you grief.
                   :
          Warnings : Drive mapping passwords are clear text within the script.
                   :  
                   :
    Last Update by : Kenneth C. Mazie (email kcmjr AT kcmjr.com for comments or to report bugs)
   Version History : v1.0 - 05-03-12 - Original
    Change History : v2.0 - 11-15-12 - Minor edits  
                   : v3.0 - 12-10-12 - Converted application commands to arrays
                   : v4.0 - 02-14-13 - Converted all other sections to arrays
                   : v4.1 - 02-17-13 - Corrected error with pop-up notifications
                   : v5.0 - 03-05-13 - Changed notifications into functions as well as
                   :                   load routines.  Added extra load options.  Fixed bugs.
                   :
=======================================================================================#>
