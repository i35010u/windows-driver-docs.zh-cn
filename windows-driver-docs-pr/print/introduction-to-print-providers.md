---
title: 若要打印提供程序的简介
description: 若要打印提供程序的简介
ms.assetid: a0e5e8c8-7af4-4715-9036-64ae851b307d
keywords:
- 有关打印提供程序的打印提供商 WDK，
- 打印作业 WDK、 打印提供程序
- 打印提供商 WDK，数据流路径
- OpenPrinter
- 作业 WDK 打印、 打印提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e43c86a73678fe6841147b08f883826224914990
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546814"
---
# <a name="introduction-to-print-providers"></a>若要打印提供程序的简介

> [!WARNING]
> 从 Windows 10 开始，已弃用的 Api 支持第三方打印提供程序。 Microsoft 不建议到第三方打印提供商的任何投资。 此外，在 Windows 8 和更高版本的 v4 打印驱动程序模型是可用的产品，第三方打印提供商不可能创建，或管理使用 v4 打印驱动程序的队列。

打印提供商将负责将定向到本地或远程打印设备打印作业。 它们也要负责打印队列管理操作，如启动、 停止和枚举服务器的打印队列。 打印提供商定义的打印服务器的高级别、 独立于计算机的、 独立于操作系统的视图。

所有打印提供程序实现的一组公共[打印提供程序的功能](print-provider-capabilities.md)。 这些功能由一组 API 函数，由后台处理程序的路由器 (Spoolss.dll) 调用的定义。

定义的打印提供商的大多数函数要求打印机句柄作为输入。 后台处理程序客户端通过调用获取打印机句柄**OpenPrinter** （Microsoft Windows SDK 文档中所述） 中 Winspool.drv，它调用 API 服务器 (Spoolsv.exe)。 后台处理程序的路由器 (Spoolss.dll) 将调用每个打印提供商**OpenPrinter**函数直到其中一个提供打印机句柄并返回值，该值指示打印提供程序识别指定的打印机名称。 路由器然后返回到 API 服务器的其自己的句柄。 路由器的句柄包括打印机句柄和提供程序句柄。 此句柄返回给应用程序，以便从应用程序的后续调用可以定向到正确的访问接口和打印机。

Microsoft 提供了以下打印提供程序与 Windows 2000 及更高版本：

**Localspl.dll**  
[本地打印提供程序](local-print-provider.md)。 所有打印作业定向到本地服务器中托管的打印机的句柄。

**Win32spl.dll**  
Windows 网络打印提供程序。 句柄打印作业定向到远程 Win32 （NT 基于操作系统的系统或 Windows 工作组） 服务器。 当作业在远程服务器到达时，则将它传递到服务器的本地打印提供程序。

**Nwprovau.dll**  
Novell NetWare 打印提供程序。 句柄打印作业定向到 Novell NetWare 打印服务器。

**Inetpp.dll**  
HTTP 打印提供程序。 句柄打印作业发送到的 URL。

供应商可以创建其他网络打印提供商。 有关详细信息，请参阅[编写网络打印提供商](writing-a-network-print-provider.md)。

下图说明了可能的数据流路径涉及这些打印提供程序。

![打印提供程序数据流路径 ](images/flowpths.png)

在查看关系图时，应考虑以下几点：

-   如果打印机由客户端系统，由处理打印作业[本地打印提供程序](local-print-provider.md)(Localspl.dll)。 管理的 Localspl.dll 打印机就不必是物理上的本地客户端，则它们可以直接连接到网卡。

-   如果打印机位于 NT 基于操作系统的系统服务器上，网络提供商 (Win32spl.dll) 使用 RPC 调用重定向从客户端的路由器到服务器的 Spoolsv.exe 进程。 由于该打印机是服务器本地，本地服务器的打印提供程序将会处理打印作业。

-   如果某些其他类型的服务器位于打印机，则可以通过哪种本地打印提供程序或支持该服务器类型，使用数据的格式和支持的服务器网络协议的网络打印提供程序访问。

-   对于本地打印的提供程序来访问远程打印机，它必须包含[端口监视器](https://docs.microsoft.com/windows-hardware/drivers/print/port-monitors)，可以使用远程打印机或服务器识别的网络协议。
