---
title: 打印提供程序简介
description: 打印提供程序简介
ms.assetid: a0e5e8c8-7af4-4715-9036-64ae851b307d
keywords:
- 打印提供程序 WDK，关于打印提供程序
- 打印作业 WDK，打印提供程序
- 打印提供程序 WDK，流路径
- OpenPrinter
- 作业 WDK 打印，打印提供程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c3ea1c5b98c682237254fd223bdc6e1347359fb
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213129"
---
# <a name="introduction-to-print-providers"></a>打印提供程序简介

> [!WARNING]
> 从 Windows 10 开始，不推荐使用支持第三方打印提供程序的 Api。 Microsoft 不建议对第三方打印提供商进行任何投资。 此外，在可用 v4 打印驱动程序模型的 Windows 8 和更高版本产品上，第三方打印提供商可能不会创建或管理使用 v4 打印驱动程序的队列。

打印提供程序负责将打印作业定向到本地或远程打印设备。 它们还负责打印队列管理操作，例如启动、停止和枚举服务器的打印队列。 打印提供程序定义了打印服务器的高级、独立于计算机的、独立于操作系统的视图。

所有打印提供程序都实现一组通用的 [打印提供程序功能](print-provider-capabilities.md)。 这些功能由一组 API 函数定义，这些函数由后台处理程序的路由器调用 ( # A0) 。

打印提供程序定义的大多数函数需要一个打印机句柄作为输入。 后台处理程序客户端通过调用 Microsoft Windows SDK 文档) 的文档中所述的 **OpenPrinter** (获取打印机句柄，该文档将调用 API 服务器 ( # A0) 。 后台处理程序的路由器 ( # A0) 会调用每个打印提供程序的 **OpenPrinter** 函数，直到其中一个提供程序提供打印机手柄，并返回一个指示打印提供程序识别指定打印机名称的返回值。 然后，路由器会将其自己的句柄返回到 API 服务器。 路由器的句柄包括打印机句柄和提供程序句柄。 此句柄返回到应用程序，以便可以将应用程序的后续调用定向到正确的提供程序和打印机。

Microsoft 提供了以下 Windows 2000 和更高版本的打印提供程序：

**Localspl.dll**  
[本地打印提供程序](local-print-provider.md)。 处理定向到从本地服务器管理的打印机的所有打印作业。

**Win32spl.dll**  
Windows 网络打印提供程序。 处理定向到远程 Win32 (基于 NT 的操作系统或适用于工作组) 服务器的 Windows 的打印作业。 当作业到达远程服务器时，它将传递给服务器的本地打印提供程序。

**Nwprovau.dll**  
Novell NetWare 打印提供程序。 处理定向到 Novell NetWare 打印服务器的打印作业。

**Inetpp.dll**  
HTTP 打印提供程序。 处理发送到 URL 的打印作业。

供应商可以创建更多的网络打印提供商。 有关详细信息，请参阅 [编写网络打印提供程序](writing-a-network-print-provider.md)。

下图说明了涉及这些打印提供程序的可能的流路径。

![打印提供程序流路径 ](images/flowpths.png)

查看关系图时，应考虑以下几点：

-   如果打印机由客户端系统进行管理，则打印作业由 [本地打印提供程序](local-print-provider.md) 处理 ( # A0) 。 Localspl.dll 管理的打印机不必在物理上本地到客户端;它们可以直接连接到网卡。

-   如果打印机位于基于 NT 的操作系统服务器上，则网络提供程序 ( # A0) 使用 RPC 将来自客户端路由器的调用重定向到服务器的 Spoolsv.exe 进程。 因为打印机是服务器本地的，所以服务器的本地打印提供程序将处理打印作业。

-   如果打印机位于某种其他类型的服务器上，则可以通过本地打印提供程序或支持该服务器类型的网络打印提供程序访问该打印机，使用服务器支持的数据格式和网络协议。

-   为了使本地打印提供程序能够访问远程打印机，它必须包含可使用远程打印机或服务器识别的网络协议的 [端口监视器](./port-monitors.md) 。