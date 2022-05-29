# PERFECTwall

## La version Française se trouve ici : [README_FR.md](https://github.com/Captain-FLAM/PERFECTwall/blob/master/README_FR.md)

The first 100% open-source Firewall for Windows 7/8/10 !

This project is open to any form of participation (Developers, Bloggers, Sponsors, etc.)

### BIOGRAPHY

Programmer since the age of 12 (1981).  
Before, I developed in ASM, C, C++, Basic, Visual Basic.  
Since the year 2000, I have been coding in PHP, MySQL, JavaScript, jQuery, HTML, CSS.  
And today in C# for this project.

### HISTORY

In Windows 98 and XP, I used « Kerio Firewall » and in Windows 7, « PC Tools Firewall ».  
Those two worked out well for me, as they displayed the URL requested by each software.

But since Windows 10, it's a disaster !

All current firewalls running under Windows 10 are IP oriented (the one integrated into Windows, Comodo, ZoneAlarm, TinyWall, Outpost, ...)

Other than « Free Firewall » (from Evorim), but that doesn't work well, only checks outgoing connections, and isn't open-source.

And aside from « PortMaster », which I just discovered recently and which fits my idea, but is written in GO and downloads 300MB of dependencies !  
Some will be fully satisfied with this solution, that you can see here : [github.com/safing/portmaster](https://github.com/safing/portmaster)

But this is very far from the idea that I have of a Firewall that is light, fast and takes up little space in memory !!

### REPORT

1. From the very first Windows I used (version 3.1) until today, I have never known a **100% Open-Source** Firewall !
2. I think it's nonsense to block IPs, because one server can host multiple websites under the same IP !
3. In addition, how do you know if you want to authorize a firewall rule without knowing what the displayed IP corresponds to (without bothering to do a web search) ?

Solution : Block domain names instead, or groups of server IPs belonging to companies.

### AN OLD DREAM

Since 2014, I've been dreaming of an ideal firewall and I've collected a whole lot of information and source codes, but I haven't found anything convincing.  
Recently, I've been browsing the archives of my captured files and it made me want to see what's new on the web...  
During hazardous researchs, I came across a driver that may correspond to my filtering criteria and from there, here I am again on this crazy project !

### THE IDEAL FIREWALL ?

I dream of a Firewall that advises me intelligently on what I should decide and that does not harass me too much, while ensuring my peace of mind...

It would be an application firewall (different rules per application, which is already the case for most) but with filtering by domain names, or by IP groups, or by IP if necessary.  
For instance :  
Allow « Windows Update » to connect to Microsoft-owned IPs ONLY.  
Deny « Firefox » connection to Mozilla ping service.  
Deny « Windows » connection to Microsoft « Account » service. ( → login.live.com)

With simple global rules, for example :  
Globally allow/deny services needed for « Windows Update » (BITS, WuauServ, Orchestrator, etc.)  
No more hacks in the registry to prevent untimely updates !  
Thus, my Windows would update ONLY when I decided !

and of course :  
Completely deny a program to connect to the internet !  
(i.e.: no DNS queries either : time saving, less waiting threads, battery saving on laptops, more network bandwidth available, less electrical pollution, etc.)

Believe me, if you knew the number of useless connections per minute, per hour, per day that leave your PC, you would be amazed !  
Moreover, thanks to **PERFECTwall**, you will realize it.

Multiply that by billions of PCs...  
To reduce global warming, let's start by reducing the access of our PCs !!

### MINIMUM REQUIREMENTS

1. Windows 8, Windows 8.1, Windows 10
2. Visual C++ Runtime 2015
3. .NET Framework 4.52

[2] - If you don't have this library installed, you can [download it here](https://www.microsoft.com/en-in/download/details.aspx?id=48145) (14 Mo) or the [newer version](https://docs.microsoft.com/en-us/cpp/windows/latest-supported-vc-redist?view=msvc-170) 2015-2022 (25 MB)

[3] - .NET version 4.52 is automatically installed with Windows 8.1.  
For Windows 10 : there is nothing to do.  
For Windows 8 : update to [version 4.52](https://dotnet.microsoft.com/en-us/download/dotnet-framework/net452) (or +)

### SOLUTIONS USED

**PERFECTwall** is coded in C# for rapid prototyping, but the driver (WinDivert) is coded in C.  
Subsequently, some parts can be recoded in C or C++ to be more efficient.

I chose to use .NET version 4.5.2 at minimum so that people don't need to install any dependencies other than Visual C++ (14MB minimum, even not at all if there is already a higher version installed).

**WinDivert** - (coded in C)  
This awesome driver which is developed by « Basil00 », and whose I modified the DLL to make the driver installation permanent in "C:\Windows\System32".

> Windows Packet Divert (WinDivert) is a user-mode packet interception library
> for Windows 7, Windows 8 and Windows 10.
>
> In summary, WinDivert can:
> - capture network packets
> - filter/drop network packets
> - sniff network packets
> - (re)inject network packets
> - modify network packets

**WinDivertSharp** - (coded in C#)  
I started from the work done by « TechnikEmpire » who had created this interface for version 1.4 of Windivert and I deeply took over all the code to make it working with version 2.2 of WinDivert, and I simplified and standardized it .

I included just the necessary in this project, but if you want to see the rest (examples, tests and others) :  
[github.com/basil00/Divert](https://github.com/basil00/Divert)  
[github.com/TechnikEmpire/WinDivertSharp](https://github.com/TechnikEmpire/WinDivertSharp)

### ROADMAP

- Block domain names per application.
- To verify or not to verify domain names by application.  
(e.g : Do not check for BitTorrent.exe, because connections are made by IP)
- Redirect requests by domain name and by protocol.  
(e.g : www.XXX.com port 80 → 127.0.0.1 port 64080 : HTML page returned « Connection blocked »)
- Allow/Block requests by business groups (avoid telemetry, DNS poisoning, etc.)
- Simply allow/deny necessary services by groups, day by day.  
(e.g : Local Area Network (LAN), Windows Update, Visual Studio, etc.)
- Intelligently advise on actions to take for obscure Windows services with a comprehensive information panel.  
(e.g : Netbios connection → « Are you using a local network? » YES/NO : Disallow all local network services at once)
- And in the future and for the most paranoid of you (like me) who don't trust Microsoft's WFP, I would like to be able to develop an NDIS 6.0 driver in the same spirit as « WinpkFilter » (which is not open-source)

Bonus : I like to see my network activity at a glance and apart from Comodo none have a visual indicator, except of course **PERFECTwall** !

### COMPILATION

To compile this program, you will need :

[Visual Studio (Community)](https://visualstudio.microsoft.com/en/) which is free.  
[.NET Framework 4.5.2 Developer Pack](https://www.microsoft.com/en-us/download/details.aspx?id=42637)  
OR a [higher version](https://dotnet.microsoft.com/en-us/download/visual-studio-sdks) ( 4.6.2 to 4.8 )

P.S. :  
Before someone asks me : I know that some firewalls offer additional features (digital signature verification, anti-intrusion, etc.) but it is not planned for the moment in this project.

**&copy; Captain FLAM - 2022**  
@ MIT license
