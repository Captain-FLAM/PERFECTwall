# ![](https://github.com/Captain-FLAM/PERFECTwall/wiki/images/PerfectWall.png) PERFECT wall [![](https://img.shields.io/github/stars/Captain-FLAM/PERFECTwall?color=ff0080&style=for-the-badge)](https://github.com/Captain-FLAM/PERFECTwall/stargazers) [![](https://img.shields.io/github/license/Captain-FLAM/PERFECTwall?style=for-the-badge)](https://github.com/Captain-FLAM/PERFECTwall/blob/master/LICENSE)

#### Version Française -> [README_FR.md](https://github.com/Captain-FLAM/PERFECTwall/blob/master/README_FR.md)

****

#### The first 100% open-source Firewall for Windows 8/10/11 based on domain names !

#### Motto : « Let's free the bandwidth ! »

I need help to move forward faster : This project is open to all goodwill.

You can reach  me by [email](https://github.com/Captain-FLAM) or through the module [Discussions of GitHub](https://github.com/Captain-FLAM/PERFECTwall/discussions)

# 🔥 FEATURES
### Version 0.5 (Still working on it)

✔️ Multilingual - French & English, for now  
_(You will be able to add languages very easily thanks to simple INI files encoded in UTF-8.)_

✔️ Shows DNS queries before they are sent  
_(For now, this is a simple list (log type))_

✔️ Indicates in real-time network connections on the taskbar icon  
.

# 🚀 INSTALLATION

Follow the guide in the [WIKI](https://github.com/Captain-FLAM/PERFECTwall/wiki/Installation)

# 🧒 BIOGRAPHY

Programmer since the age of 12 (1981).  
Before, I developed in ASM, C, C++, Basic, Visual Basic.  
Since the year 2000, I have been coding in PHP, MySQL, JavaScript, jQuery, HTML, CSS.  
And today in C# for this project.

# ✨ HISTORY

In Windows 98 and XP, I used « Kerio Firewall » and in Windows 7, « PC Tools Firewall ».  
Those two worked out well for me, as they displayed the URL requested by each software.

But since Windows 10, it's a disaster !

All current firewalls running under Windows 10 are IP oriented (Comodo, ZoneAlarm, Outpost, and the one integrated into Windows and those who use it : WFC from Binisoft, TinyWall, WFN from WoKhan, ...)

Other than « Free Firewall » (from Evorim), but that doesn't work well, only checks outgoing connections, and isn't open-source.

And aside from « PortMaster », which I just discovered recently and which fits my idea, but is written in GO and downloads 300MB of dependencies !  
Some will be fully satisfied with this solution, that you can see here : [github.com/safing/portmaster](https://github.com/safing/portmaster)

But this is very far from the idea that I have of a Firewall that is light, fast and takes up little space in memory !!

# 💡 REPORT

1. From the very first Windows I used (version 3.1) until today, I have never known a **100% Open-Source** Firewall based on domain names !
2. I think it's nonsense to block IPs, because one server can host multiple websites under the same IP !
3. In addition, how do you know if you want to authorize a firewall rule without knowing what the displayed IP corresponds to (without bothering to do a web search) ?

Solution : Block domain names instead, or groups of server IPs belonging to companies.

# 💤 AN OLD DREAM

Since 2014, I've been dreaming of an ideal firewall and I've collected a whole lot of information and source codes, but I haven't found anything convincing.  
Recently, I've been browsing the archives of my captured files and it made me want to see what's new on the web...  
During hazardous researchs, I came across a driver that may correspond to my filtering criteria and from there, here I am again on this crazy project !

# 💗 THE IDEAL FIREWALL ?

I dream of a Firewall that advises me intelligently on what I should decide and that does not harass me too much, while ensuring my peace of mind...

It would be an application firewall (different rules per application, which is already the case for most) but with filtering by domain names, or by IP groups, or by IP if necessary.

Individual rules :

- Allow « Windows Update » to connect to Microsoft-owned IPs ONLY.
- Deny « Firefox » connection to Mozilla ping service.
- Deny « Windows » connection to Microsoft « Account » service. ( → login.live.com)

Simple group rules, by e.g :

- Globally allow/deny services needed for « Windows Update » (BITS, WuauServ, Orchestrator, etc.)  
No more hacks in the registry to prevent untimely updates !  
Thus, my Windows would update ONLY when I decided !

and of course :

- Completely deny a program to connect to the internet !  
(no DNS queries either : time saving, less waiting threads, battery saving on laptops, more network bandwidth available, less electrical pollution, etc.)

Believe me, if you knew the number of useless connections per minute, per hour, per day that leave your PC, you would be amazed !  
Moreover, thanks to **PERFECT wall**, you will realize it.

Multiply that by billions of PCs...  
To reduce global warming, let's start by reducing the access of our PCs !!

# 🍔 SOLUTIONS

**PERFECT wall**  
**&copy; Captain FLAM - 2022**  
Coded in C# with WFP/XAML for rapid prototyping, but the driver (WinDivert) is coded in C.  
Subsequently, some parts can be recoded in C or C++ to be more efficient.

I chose to use .NET version 4.5 at minimum so that people don't need to install any dependencies other than Visual C++ (14MB minimum, even not at all if there is already a higher version installed).

**WinDivert** - (coded in C)  
**&copy; Basil00**  
This driver is awesome !  
I just modified the DLL to make the driver installation permanent in "C:\Windows\System32".
I also created an install process (install.cmd & setup.exe) to make things easier.

> WinDivert is a user-mode packet interception library for Windows 7 / 8 / 10, that can :
>
> - capture network packets
> - filter/drop network packets
> - sniff network packets
> - (re)inject network packets
> - modify network packets

**WinDivertSharp** - (coded in C#)  
**&copy; Jesse Nicholson « TechnikEmpire » - (Ontario, Canada)**  
This interface was created for version 1.4 of Windivert and I deeply took over all the code to make it working with version 2.2 of WinDivert, and morevover I simplified it.

**Hardcodet NotifyIcon for WPF** - (coded in C# / WPF / XAML)  
**&copy; Philipp Sumi - (Switzerland)**  
I had to adapt the code of the last version (1.1.0) so that it works with the .NET Framework 4.5.  

> This is an implementation of a NotifyIcon (aka system tray icon or taskbar icon) for the WPF platform.  
> It does not just rely on the Windows Forms NotifyIcon component, but is a purely independent control  
> which leverages several features of the WPF framework in order to display rich tooltips, popups,  
> context menus, and balloon messages.

**INI File Parser** - (coded in C#)  
**&copy; Ricardo Amores Hernández - (Barcelona)**  
This library does not rely on Win32 APIs, and therefore supports UTF-8.  
I added the backup function which was missing on the last version.

### And a special thanks to :

**&copy; Jerome Saliba (Khan)**  
for his project which inspired me and from which I stole bits of code :  
**Windows Firewall Notifier**  
https://github.com/wokhansoft/WFN  
_(you will be able to see its copyleft in the source code of the **Process.cs** file, for example)_

---

I included just the necessary in this project, but if you want to see the rest (examples, tests and others) :  
[github.com/basil00/Divert](https://github.com/basil00/Divert)  
[github.com/TechnikEmpire/WinDivertSharp](https://github.com/TechnikEmpire/WinDivertSharp)  
[github.com/hardcodet/wpf-notifyicon](https://github.com/hardcodet/wpf-notifyicon)  
[github.com/rickyah/ini-parser](https://github.com/rickyah/ini-parser)

# 🦄 IN THE NEAR FUTURE

- Block domain names per application.
- To verify or not to verify domain names by application.  
(e.g : Do not check for BitTorrent.exe, because connections are made by IP)
- Allow/Block requests by business groups (avoid telemetry, DNS poisoning, etc.)
- Simply allow/deny necessary services by groups, day by day.  
(e.g : Local Area Network (LAN), Windows Update, Visual Studio, etc.)
- Intelligently advise on actions to take for obscure Windows services with a comprehensive information panel.  
(e.g : Netbios connection → « Are you using a local network? » YES/NO : Disallow all local network services at once)
- And in the future and for the most paranoid of you who don't trust Microsoft's WFP, I would like to be able to develop an NDIS 6.0 driver in the same spirit as « WinpkFilter » (which is not open-source)

**Bonus** : I like to see my network activity at a glance and apart from Comodo none have a visual indicator, except of course **PERFECT wall** !

# 🏗️ COMPILATION

Follow the guide in the [WIKI](https://github.com/Captain-FLAM/PERFECTwall/wiki/Compilation)

## ➕ P.S.

Before someone asks me : I know that some firewalls offer additional features (digital signature verification, anti-intrusion, etc.) but it is not planned for the moment in this project.

### &copy; Captain FLAM - 2022 - MIT license

****

**Icons found on "Pixabay.com"**  
Shield by <a href="https://pixabay.com/fr/users/openclipart-vectors-30363/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=154885">OpenClipart-Vectors</a>  
Parameters by <a href="https://pixabay.com/fr/users/openicons-28911/?utm_source=link-attribution&amp;utm_medium=referral&amp;utm_campaign=image&amp;utm_content=98391">OpenIcons</a>