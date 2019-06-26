---
title: WIA 微型驱动程序调试
description: WIA 微型驱动程序调试
ms.assetid: 6466d0db-a2f9-4b3e-aa3e-8030b243f862
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de83d900e29497ee740d7749eb35a7445d8b9855
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355196"
---
# <a name="wia-minidriver-debugging"></a>WIA 微型驱动程序调试





WIA 服务进程内执行 WIA 驱动程序。 因此，若要执行这些驱动程序的调试用户模式下，您必须将调试器连接到 WIA 服务。 有几种不同的方法要这样做;本主题介绍了其中两个。 （请参阅 Microsoft Windows SDK 文档的其他信息中调试服务）。

可在两种方式之一启动您的调试器：

-   通过自动启动在调试器下的 WIA 服务。

-   通过在运行时将调试器附加到相应的进程。

以下是两个点，请记住：

如果您需要网络访问的符号和在调试器中的其他文件，这些可能不会显示如果在调试器下的 WIA 服务自动启动。 WIA 为 Windows XP 中的本地系统服务和以 localservice 身份运行 Microsoft Windows Server 2003 和更高版本的操作系统版本，并且没有适当的权限来访问网络。 因此，即使你的计算机可以"看到"的所有内容在网络上，可能无法再到调试器运行服务。 有关 WIA 服务的详细信息的更改的权限级别，请参阅[WIA 驱动程序的安全问题](security-issues-for-wia-drivers.md)。

-   如果驱动程序加载或初始化该驱动程序的 STI 部分期间出现问题 (例如，在为[ **IStiUSD::Initialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-initialize))，然后附加调试器时，该错误已有发生并已经太迟以获得有用的信息。 此问题的常见症状是，设备不会不会显示在**我的电脑**文件夹中，但*does*显示在**设备管理器**文件夹。

### <a name="starting-the-wia-service-under-a-debugger"></a>启动在调试器下 WIA 服务

WIA 服务启动时，服务控制管理器 (SCM) 看起来在服务管理数据库中的条目，并启动该条目指向可执行文件。 启动调试程序下的 WIA 服务的简单方法是将该条目替换为一个包含您的调试器。 可以在注册表中找到该条目：

**HKLM\\System\\CurrentControlSet\\Services\\StiSvc\\ImagePath**

最初， **ImagePath**键设置为以下字符串值：

" **%SystemRoot%\\System32\\svchost.exe -k imgsvc**"

若要运行 NTSD WIA 服务，例如，按如下所示修改上面的值：

"**ntsd -g -G %SystemRoot%\\System32\\svchost.exe -k imgsvc**"

进行此更改后，WIA 服务始终在 NTSD 下启动。 请注意，是否已在运行该服务，它必须停止并重新启动此更改才能生效。 请参阅[启动和停止静止图像服务](starting-and-stopping-the-still-image-service.md)有关详细信息。

若要使调试器的窗口可见，还需要更改另一个注册表项。 对此注册表项的路径为：

**HKLM\\System\\CurrentControlSet\\Services\\StiSvc\\Type**

初始值**类型**密钥，0X20，阻止显示在调试器窗口。 更改的值**类型**为 DWORD 值 0X120 密钥。

### <a name="attaching-the-debugger-at-run-time"></a>将调试器附加在运行时

大多数调试器需要才能将连接到该进程已启动后正在运行的进程的 PID。 因为名为泛型宿主进程下运行 WIA *svchost.exe*，查找正确的实例*svchost.exe*至关重要。

如果从 Microsoft 网站 (www.microsoft.com) 下载调试器包，它包含名为的实用程序*tlist.exe*。 *Tlist.exe*显示所有正在运行的进程。 如果您执行*tlist.exe*使用 s 开关，此实用工具还显示哪些进程托管的服务。 例如，运行*tlist.exe s*生成类似于以下输出：

```console
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

在前面的示例中，五个实例的*svchost.exe*正在运行。 WIA 服务**StiSvc** （静止图像服务） 下运行*svchost.exe*其 PID 是 1076年的实例。 将调试器附加到进程 1076 开始调试。

而不是使用一个实用程序，如*tlist.exe，* 标识的多个单个实例*svchost.exe*情况下，您可以制作一份*svchost.exe*和重命名它 (例如， *stisvc.exe*)。 然后，将更改的服务控制条目**ImagePath**要使用此副本的值*svchost.exe* (其名称现在是的一个*stisvc.exe*)。 例如，可以设置其路径的键

**HKLM\\System\\CurrentControlSet\\Control\\Services\\Stisvc\\ImagePath**

为以下字符串值：

" **%SystemRoot%\\System32\\stisvc.exe -k imgsvc**"

现在，当 WIA 服务启动时，它运行下*stisvc.exe*而不是*svchost.exe*。 查找此过程是更简单，因为没有单个实例的*stisvc.exe*。 无需查找 PID 查找它。 因此，例如，如果你要开发使用 Microsoft Visual Studio 的驱动程序，则可以转到**开始调试**下的菜单项**构建**菜单中，单击**附加到进程...** ，然后选择*stisvc.exe*列表中。
