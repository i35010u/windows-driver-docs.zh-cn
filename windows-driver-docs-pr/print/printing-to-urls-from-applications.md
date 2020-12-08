---
title: 从应用程序打印到 URL
description: 从应用程序打印到 URL
keywords:
- Internet 打印 WDK，打印到 Url
- URL 标识的打印队列 WDK
- 友好名称 WDK 打印机
- 打印到 Url WDK
- 打印网页 WDK，打印到 Url
- 网页 WDK 打印机，打印到 Url
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23ee927c64541c894114e06734036df60c6ab9ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807213"
---
# <a name="printing-to-urls-from-applications"></a>从应用程序打印到 URL





从应用程序的角度来看，打印到 URL 标识的打印队列与打印到 UNC 识别的打印队列完全相同。 应用程序通常不知道通过 URL 访问打印队列。

通过 [查看打印网页](viewing-print-web-pages.md)，用户可以安装并连接到 URL 标识的打印队列。 发生这种情况时，会为打印队列分配与打印服务器上相同的 "友好名称"，此友好名称将在用户的打印文件夹中列出。

通常，应用程序通过其友好名称来引用打印队列，这与 UNC 识别的打印队列一样。 对本地打印提供程序中的 **OpenPrinter** 函数的调用 (引起的，例如，使 GDI 调用) 的应用程序包括友好名称。 同时，本地打印提供程序会调用 HTTP 打印提供程序中的 **OpenPrinter** ， ( # A0) 指定打印队列的 URL。

使用友好名称引用打印队列的应用程序通常不知道打印队列是本地还是网络，或者网络协议是 RPC、SMB 还是 HTTP。 但是，应用程序可以根据需要直接调用 **OpenPrinter** ，并指定一个 URL。 指定 **OpenPrinter** 的 url 时，必须使用以下 URL 格式：

https:// &lt; ServerName &gt; /printers/ &lt; 共享 &gt; /.printer

其中 &lt; ServerName &gt; 是服务器名称 (Internet 连接的 DNS 名称，或) intranet 连接的 WINS 名称，"打印机" 表示服务器上的虚拟目录，而 &lt; 共享名 &gt; 是打印队列的共享名，如其属性表中所指定。 Microsoft Windows SDK 文档中讨论 (虚拟目录。 ) 

当客户端后台处理程序组件或应用程序调用 **OpenPrinter** 并指定 URL 时，对后台处理程序函数的后续调用（如 **StartDocPrinter**、 **WritePrinter** 等）由客户端的 HTTP 打印提供程序处理。 HTTP 打印提供程序将参数追加到 URL，并将生成的 URL 字符串发送到打印服务器。

对于 Microsoft Windows 2000 打印服务器，若要接受包含 Url 的打印请求，则必须运行以下任一操作：

-   带有 Microsoft Internet Information Server (IIS) 或的 Windows 2000 服务器软件

-   Windows 2000 Professional software with Microsoft 对等 Web 服务器

对于 Windows XP 打印服务器，若要接受包含 Url 的打印请求，则必须运行以下任一操作：

-   带有 Microsoft Internet Information Server (IIS) 或的 microsoft Windows Server 2003 软件

-   Windows XP Professional software with Microsoft 对等 Web 服务器

**注意**   Windows XP Home Edition 打印服务器无法接受包含 Url 的请求。

 

在打印服务器上，IIS 或对等 Web 服务器接收 URL 字符串。 通过在客户端系统上 Inetpp.dll 追加到字符串后面的参数会导致服务器调用 HTTP 打印服务器，该服务器包含在 Msw3prt.dll 中。 HTTP 打印服务器接受原始格式的打印机数据并将其发送到本地打印后台处理程序。

使用 Internet 设计协议 (IPP 1.0) ，将打印机数据从客户端发送到服务器，) Internet 工程任务 (组 (IETF) 。

下图说明了当客户端打印到 URL 标识的打印队列时，打印数据从客户端应用程序到打印服务器后台处理程序的路径。

![说明如何打印到 url 标识的打印队列的关系图](images/prntpath.png)

如果客户端和服务器都是 Windows 2000 或更高版本的系统（如图所示），则通常 (RPC 协议，但并不总是) 用于客户端-服务器通信。  (有关详细信息，请参阅 [从网页安装打印驱动程序](installing-print-drivers-from-a-web-page.md)。 ) 如果客户端和服务器不是 Windows 2000 或更高版本的系统，将使用 HTTP。 HTTP 还用于包含内部网卡并支持 IPP 1.0 的打印机，因此未连接到服务器。

打印服务器安全性由 IIS 提供，后者在打印服务器上执行。 Iis *资源指南* 中介绍了 iis 支持的安全机制，其中包含于 * *

*Microsoft Windows 2000 服务器资源工具包*。 此外，资源工具包还明确说明了系统管理员如何控制与打印到 Url 相关联的安全方法。

 

 




