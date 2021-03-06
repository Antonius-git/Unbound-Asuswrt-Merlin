# unbound Manager/Installer script for ASUS Router running RMerlin firmware.

## Installation ##

Enable SSH on router, then use your preferred SSH Client e.g. Xshell6,MobaXterm, PuTTY etc. to copy'n'paste:

	mkdir /jffs/addons 2>/dev/null;mkdir /jffs/addons/unbound 2>/dev/null; curl --retry 3 "https://raw.githubusercontent.com/MartineauUK/Unbound-Asuswrt-Merlin/master/unbound_manager.sh" -o "/jffs/addons/unbound/unbound_manager.sh" && chmod 755 "/jffs/addons/unbound/unbound_manager.sh" && /jffs/addons/unbound/unbound_manager.sh


#### To execute the utility, you may then use the _alias_ ####

	unbound_manager

#### NOTE: For a standard screen display 1024x768 (or its modern popular equivalent 1366×768), using Xshell6/MobaXterm, you can dynamically change the font size using the CTRL+Mouse-scroll wheel to have a full-screen recommended unbound_manager window 191x37
#### If using PuTTY I suggest you use PuTTY-url (v0.73) and manually set the unbound_manager window size 191x37 with font 'Terminal 9-point' (unbound_manager can/will display clickable URLs and basic PuTTY won't open the links)


```
+======================================================================+
|  Welcome to the unbound Manager/Installation script (Asuswrt-Merlin) |
|  Version 2.01 by Martineau                                           |
|                                                                      |
| Requirements: USB drive with Entware installed                       |
|                                                                      |
|   i = Install unbound DNS Server - Advanced Mode                     |
|       o1. Enable unbound Logging                                     |
|       o2. Integrate with Stubby                                      |
|       o3. Install Ad and Tracker Blocking                            |
|       o4. Customise CPU/Memory usage (Advanced Users)                |
|       o5. Disable Firefox DNS-over-HTTPS (DoH) (USA users)           |
|                                                                      |
|   z  = Remove Existing unbound Installation                          |
|   ?  = About Configuration                                           |
|                                                                      |
| You can also use this script to uninstall unbound to back out the    |
| changes made during the installation. See the project repository at  |
|         https://github.com/rgnldo/unbound-Asuswrt-Merlin             |
|     for helpful user tips on unbound usage/configuration.            |
+======================================================================+


unbound (pid 3113) is running... uptime: 0 Days, 01:14:24 version: 1.9.3 (# rgnldo User Install Custom Version vx.xx (Date Loaded by unbound_installer Fri Jan 10 11:43:15 GMT 2020))


i  = Update unbound Installation ('/opt/var/lib/unbound/')      l  = Show unbound LIVE log entries (lx=Disable Logging)
z  = Remove Existing unbound Installation                       v  = View ('/opt/var/lib/unbound/') unbound Configuration (vx=Edit; vh=View Example Configuration) 
3  = Advanced Tools                                             rl = Reload Configuration (Doesn't halt unbound) e.g. 'rl test1[.conf]' (Recovery use 'rl reset/user')
?  = About Configuration                                        oq = Query unbound Configuration option e.g 'oq verbosity' (ox=Set) e.g. 'ox log-queries yes'

rs = Restart (or Start) unbound                                 s  = Show unbound statistics (s=Summary Totals; sa=All; s+=Enable Extended Stats)

e  = Exit Script


A:Option ==> ?

	Version=2.01
	Local						md5=2522e397a5bb40529acbd3722b50fcee
	Github						md5=2522e397a5bb40529acbd3722b50fcee
	/jffs/addons/unbound/unbound_manager.md5	md5=2522e397a5bb40529acbd3722b50fcee



```

##### New in **v1.20** is the ability to specify which *User Selectable options* are to be installed without having to _manually_ reply to each individual feature prompt

 e.g. Auto install both options 

     o4. Customise CPU/Memory usage (Advanced Users)   
     o5. Disable Firefox DNS-over-HTTPS (DoH) (USA users)  
```
e  = Exit Script

Option ==> i 5 4

<snip>

Customising Unbound configuration Options:
Option Auto Reply 'y'	Customising Unbound Performance/Memory 'proc/sys/net' parameters
	stuning downloaded successfully
Applying Unbound Performance/Memory tweaks using '/jffs/scripts/stuning'
Restarting dnsmasq.....
Done.
 Starting unbound...              done. 
Option Auto Reply 'y'	Installing Firefox DNS-over-HTTPS (DoH) DISABLE/Blocker....
	adblock/firefox_DOH downloaded successfully
Adding Firefox DoH 'include: /opt/var/lib/unbound/adblock/firefox_DOH'

<snip>

Auto install Customisation complete 0 minutes and 48 seconds elapsed - Please wait for up to 10 seconds for status.....


Option ==> ?

	Version=1.24
	Local					md5=f94581fc563a351b6caddc27607b0b3a
	Github					md5=f94581fc563a351b6caddc27607b0b3a
	/jffs/scripts/unbound_manager.md5	md5=f94581fc563a351b6caddc27607b0b3a


	Router Configuration recommended pre-reqs status:

	[✔] Swapfile=262140 kB
	[✖] ***ERROR DNS Filter is OFF!  						see http://10.88.8.1/DNSFilter.asp LAN->DNSFilter Enable DNS-based Filtering
	[✖] ***ERROR WAN: Use local caching DNS server as system resolver=YES  		see http://10.88.8.1/Tools_OtherSettings.asp ->Advanced Tweaks and Hacks
	[✖] ***ERROR Enable local NTP server=NO  					see http://10.88.8.1/Advanced_System_Content.asp ->Basic Config
	[✔] Enable DNS Rebind protection=NO
	[✔] Enable DNSSEC support=NO

	Options (Auto Reply=Y for Options '4 5'):

	[✔] Unbound CPU/Memory Performance tweaks
	[✔] Firefox DNS-over-HTTPS (DoH) DISABLE/Blocker

```
The script will remember the Auto Selected Options (for the *current* session) so you may simply specify the additional Auto install Option feature(s)

 e.g. include additional option

     o3. Ad and Tracker Blocking

```
e  = Exit Script

Option ==> i 3

<snip>

	Options (Auto Reply=Y for Options '3 4 5'):

	[✔] Ad and Tracker Blocking (No. of Adblock domains 63400, - Warning Diversion is also ACTIVE)
	[✔] Unbound CPU/Memory Performance tweaks
	[✔] Firefox DNS-over-HTTPS (DoH) DISABLE/Blocker

```
To Auto reply to **ALL** of the *Selectable User Options*, rather than _manually_ enter the complete list, simply use:

```
e  = Exit Script

Option ==> i all
```

To reinstate **ALL** *Selectable User Option* prompts issue

```
e  = Exit Script

Option ==> i?
```

**v1.21** now allows dumbing down of the menus (**'Easy Mode'**) and will be used when invoked from **amtm** 

(When invoked direct from the commandline the default is **'Advanced Mode'**)

```
+======================================================================+
|  Welcome to the unbound-Manager/Installation-Asuswrt-Merlin script   |
|  Version 1.21 by Martineau                                           |
|                                                                      |
| Requirements: USB drive with Entware installed                       |
|                                                                      |
|   1 = Install unbound DNS Server                                     |
|                                                                      |
|   2 = Install unbound DNS Server - Advanced Mode                     |
|       o1. Enable unbound Logging                                     |
|       o2. Integrate with Stubby                                      |
|       o3. Install Ad and Tracker Blocking                            |
|       o4. Customise CPU/Memory usage (Advanced Users)                |
|       o5. Disable Firefox DNS-over-HTTPS (DoH) (USA users)           |
|                                                                      |
|   3 = Advanced Tools                                                 |
|                                                                      |
| You can also use this script to uninstall unbound to back out the    |
| changes made during the installation. See the project repository at  |
|         https://github.com/rgnldo/unbound-Asuswrt-Merlin             |
|     for helpful user tips on unbound usage/configuration.            |
+======================================================================+

unbound (pid 20593) is running... uptime: 0 Days, 16:45:47 version: 1.9.3 (# rgnldo User Install Custom Version vx.xx (Date Loaded by unbound_installer Mon Jan 13 19:42:33 GMT 2020))


1  = Begin unbound Installation Process ('/opt/var/lib/unbound/')
2  = Begin unbound Advanced Installation Process ('/opt/var/lib/unbound/')
3  = Advanced Tools

 	

e  = Exit Script

E:Option ==> 

```

You can override the default **'Advanced mode'** startup i.e switch to **'Easy mode'** from the command line by using
```
unbound_manager easy
```
or you can quickly change modes at the option prompt

```
e  = Exit Script

E:Option ==> [ easy | advanced ]
```
