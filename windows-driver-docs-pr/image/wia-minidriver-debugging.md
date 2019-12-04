---
title: WIA 微型驱动程序调试
description: WIA 微型驱动程序调试
ms.assetid: 6466d0db-a2f9-4b3e-aa3e-8030b243f862
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 61711f0f18e4bf4a3855dca36ecfd83dfbb3c0cf
ms.sourcegitcommit: 1585a52e762226b01c7369371727746487cc57bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2019
ms.locfileid: "74796667"
---
# <a name="wia-minidriver-debugging"></a>WIA 微型驱动程序调试

WIA 驱动程序在 WIA 服务进程内执行。 因此，为了执行这些驱动程序的用户模式调试，必须将调试器连接到 WIA 服务。 有多种不同的方法可实现此目的;本主题介绍其中的两个。 （有关其他信息，请参阅 Microsoft Windows SDK 文档中的调试服务）。

可以通过以下两种方式之一启动调试器：

- 在调试器下自动启动 WIA 服务。

- 在运行时将调试器附加到适当的进程。

调试微型驱动程序时，请记住以下两点：

1. 如果需要从调试器中访问符号和其他文件的网络，则在调试器下自动启动 WIA 服务时，这些文件可能不可见。 WIA 作为 LocalSystem 服务在 Windows XP 和 Microsoft Windows Server 2003 及更高版本的操作系统版本中运行，并且没有访问网络的适当权限。 因此，即使您的计算机可以 "查看" 网络上的所有内容，运行该服务的调试器也可能无法运行。 有关 WIA 服务的更改权限级别的详细信息，请参阅[Wia 驱动程序的安全问题](security-issues-for-wia-drivers.md)。

1. 如果在驱动程序的 STI 部分的加载或初始化过程中出现问题（例如，在[**IStiUSD：： Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-initialize)期间），则在附加调试器时，此错误已经发生并且太晚，无法获取有用的信息。 此问题的常见症状是设备不*会显示在***我的电脑**文件夹中，而是显示在**设备管理器**文件夹中。

## <a name="starting-the-wia-service-under-a-debugger"></a>在调试器下启动 WIA 服务

WIA 服务启动后，服务控制管理器（SCM）将查看服务控制数据库中的条目，并启动该条目指向的可执行文件。 在调试器下启动 WIA 服务的一种简单方法是将该项替换为包含调试器的项。 可在以下注册表项中找到该条目：

**HKLM\\System\\CurrentControlSet\\服务\\StiSvc\\ImagePath**

最初， **ImagePath**键设置为以下字符串值：

" **% SystemRoot%\\System32\\svchost.exe-k imgsvc**"

例如，若要在 NTSD 下运行 WIA 服务，请按如下所示修改上述值：

"**ntsd-g-g% SystemRoot%\\System32\\svchost.exe-k imgsvc**"

进行此更改后，WIA 服务始终在 NTSD 下启动。 请注意，如果服务已在运行，则必须先停止并重新启动该服务，然后才能使此更改生效。 有关详细信息，请参阅[启动和停止静止映像服务](starting-and-stopping-the-still-image-service.md)。

若要使调试器窗口可见，还需要更改另一个注册表项。 此注册表项的路径为：

**HKLM\\System\\CurrentControlSet\\服务\\StiSvc\\类型**

**类型**键0x20 的初始值会阻止显示调试器窗口。 将**类型**键的值更改为 DWORD 值0X120。

### <a name="attaching-the-debugger-at-run-time"></a>在运行时附加调试器

大多数调试器都需要正在运行的进程的 PID，才能在该进程已启动之后附加到该进程。 由于 WIA 在名为*svchost.exe*的泛型宿主进程下运行，因此查找正确的*svchost.exe*实例是必不可少的。

如果从 Microsoft 站点（www.microsoft.com）下载了调试程序包，该程序包将包含一个名为*tlist.exe*的实用程序。 *Tlist.exe*显示所有正在运行的进程。 如果使用 s 开关执行*tlist.exe* ，此实用工具还会显示哪些进程正在托管哪些服务。 例如，运行*tlist.exe*会生成类似于以下内容的输出：

```cmd
   0 System Process
   4 System
 160 smss.exe
 216 csrss.exe       Title:
 208 winlogon.exe    Title: NetDDE Agent
 268 services.exe    Svcs:  Eventlog,PlugPlay
 280 lsass.exe       Svcs:  Netlogon,PolicyAgent,ProtectedStorage,SamSs
 416 svchost.exe     Svcs:  RpcSs
 444 svchost.exe     Svcs:  AudioSrv,CryptSvc,Dhcp,EventSystem,FastUserSwitching,CompatibilityServices,helpsvc,Irmon,lanmanserver,lanmanworkstation,Netman,Nla,Schedule,SENS,ShellHWDetection,srservice,TapiSrv,TermService,ThemeService,uploadmgr,W32Time,winmgmt,WmdmPmSp
 504 svchost.exe     Svcs:  Dnscache
 372 svchost.exe     Svcs:  LmHosts,Messenger,RemoteRegistry,SSDPSRV,WebClient
 616 spoolsv.exe     Svcs:  Spooler
 680 inojobsv.exe    Svcs:  Cheyenne InocuLAN Anti-Virus Server
 700 emsvc.exe       Svcs:  EMSVC
 912 fxssvc.exe      Svcs:  Fax
 192 explorer.exe    Title: Program Manager
1076 svchost.exe     Svcs:  stisvc
22824 tlist.exe
```

在前面的示例中， *svchost.exe*的五个实例正在运行。 WIA 服务**StiSvc** （静态图像服务）在其 PID 为1076的*svchost.exe*实例下运行。 将调试器附加到进程1076以启动调试。

您可以创建*svchost.exe*的副本并对其重命名（例如， *stisvc*），而不是使用*tlist.exe*等实用工具程序来标识多个*svchost.exe*实例的单个实例。 然后，将服务控制项的**ImagePath**值更改为使用此*svchost.exe*副本（其名称现在为*stisvc*）。 例如，可以设置其路径为

**HKLM\\System\\CurrentControlSet\\控件\\Services\\Stisvc\\ImagePath**

到以下字符串值：

**% SystemRoot%\\System32\\stisvc-k imgsvc**"

WIA 服务启动后，它将在*stisvc*而不是*svchost.exe*下运行。 查找此过程更简单，因为只有一个*stisvc*实例。 无需查找 PID 即可找到它。 例如，如果使用 Microsoft Visual Studio 开发驱动程序，则可以在 "**生成**" 菜单下，单击 "**启动调试**" 菜单项，单击 "**附加到进程 ...** "，然后在列表中选择 " *stisvc* "。
