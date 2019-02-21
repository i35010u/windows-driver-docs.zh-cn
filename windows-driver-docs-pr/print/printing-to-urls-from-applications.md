---
title: 从应用程序打印到 Url
description: 从应用程序打印到 Url
ms.assetid: bc9aedb4-1d64-4b70-b14b-1392f914a635
keywords:
- Internet 打印 WDK，打印到的 Url
- URL 标识打印队列 WDK
- 友好名称 WDK 打印机
- 打印到 Url WDK
- 打印网页 WDK，打印到的 Url
- 网页 WDK 打印机，打印到的 Url
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d099985ded26f5e03fa83da22de7946948b81878
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534194"
---
# <a name="printing-to-urls-from-applications"></a>从应用程序打印到 Url





从应用程序的角度来看，打印到的 URL 标识的打印队列等同于打印到 UNC 标识打印队列。 通常不知道通过 URL 访问的打印队列时的应用程序。

通过[查看打印网页](viewing-print-web-pages.md)，用户可以安装并连接到的 URL 标识的打印队列。 在此情况下，打印队列分配同一个"友好名称"，它对打印服务器，并在用户的打印文件夹中列出此友好名称。

应用程序通常指打印队列通过其友好名称与在 UNC 标识打印队列。 调用**OpenPrinter**函数在本地打印提供程序 （例如引起的由应用程序进行 GDI 调用），包括友好名称。 本地打印提供程序，反过来，调用**OpenPrinter** HTTP 打印提供程序中 (Inetpp.dll)，指定打印队列的 URL。

通常不知道的打印队列是本地或在网络中，或网络协议是 RPC、 SMB 或 HTTP 应用程序是指打印队列的友好名称。 但是应用程序，如有必要，调用**OpenPrinter**直接指定的 URL。 当指定的 URL **OpenPrinter**，必须使用以下 URL 格式：

http://&lt;ServerName&gt;/printers/&lt;ShareName&gt;/.printer

其中&lt;ServerName&gt;是服务器名称 （具有 Internet 连接的 DNS 名称或 intranet 连接的 WINS 名称），"打印机"表示在服务器上的虚拟目录和&lt;ShareName&gt;是打印队列的共享名称，指定其属性表中。 （虚拟目录将讨论 Microsoft Windows SDK 文档中。）

当客户端后台处理程序组件或应用程序调用**OpenPrinter** ，并指定一个 URL 后, 面对后台处理程序函数，如**StartDocPrinter**， **WritePrinter**，依此类推，由客户端的 HTTP 打印提供程序处理。 HTTP 打印提供程序将参数追加到 URL 并将生成的 URL 字符串发送到打印服务器。

对于以接受包含 Url 的打印请求的 Microsoft Windows 2000 打印服务器，它必须运行：

-   Windows 2000 Server 软件与 Microsoft Internet 信息服务器 (IIS)，或

-   与 Microsoft 对等 Web 服务器的 Windows 2000 Professional 软件

为了使 Windows XP 的打印服务器能接受包含 Url 的打印请求，它必须运行：

-   Microsoft Windows Server 2003 软件与 Microsoft Internet 信息服务器 (IIS)，或

-   与 Microsoft 对等 Web 服务器的 Windows XP Professional 软件

**请注意**   Windows XP Home Edition 打印服务器无法接受包含 Url 的请求。

 

在打印服务器上，IIS 或对等 Web 服务器收到的 URL 字符串。 客户端系统上由 Inetpp.dll 追加到字符串的参数会导致调用 HTTP 打印服务器，它包含在 Msw3prt.dll 的服务器。 HTTP 打印服务器接受 RAW 格式的打印机的数据，并将其发送到本地打印后台处理程序。

打印机数据从客户端发送到使用 Internet 打印协议 (IPP 1.0) 定义的打印机处理组 (PWG) Internet 工程任务组 (IETF) 的服务器。

下图说明了从打印服务器后台处理程序，客户端应用程序将打印数据的路径，如果客户端将打印到的 URL 标识的打印队列。

![说明打印到的 url 标识的打印队列的关系图](images/prntpath.png)

如果客户端和服务器是 Windows 2000 或更高版本的系统，如所示，RPC 协议通常 （但不是总是） 用于客户端-服务器通信。 (有关详细信息，请参阅[在网页上安装打印驱动程序](installing-print-drivers-from-a-web-page.md)。)如果客户端和服务器不 Windows 2000 或更高版本的系统，则使用 HTTP。 HTTP 还用于包含内部网络卡和支持 IPP 1.0，并因此不连接到服务器的打印机。

打印服务器 security 提供的 IIS，打印服务器执行。 支持的 IIS 的安全机制进行了介绍*IIS 资源指南*，其中包含在 * *

*Microsoft Windows 2000 Server Resource Kit*。 此外，资源工具包介绍专门系统管理员如何才能控制与打印到的 Url 相关联的安全方法。

 

 




