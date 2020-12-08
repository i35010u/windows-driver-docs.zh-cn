---
title: 查看打印网页
description: 查看打印网页
keywords:
- Internet 打印 WDK，查看打印网页
- 查看打印网页
- 显示打印网页
- 打印网页 WDK，查看
- 网页 WDK 打印机，查看
- 打印服务器页 WDK
- 查看打印服务器页面
- 打印 Url WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c7902b6ed04df241330e6c6a7e117541ec7cbd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831215"
---
# <a name="viewing-print-web-pages"></a>查看打印网页





对于任何类型的客户端平台上执行的任何 Internet 浏览器，用户都可以查看显示 Microsoft Windows 2000 或更高版本打印服务器及其连接的打印机状态的网页。 Microsoft 提供了一组用于生成这些网页的服务器驻留 HTML 文件。 使用 Url 的客户端浏览器可以引用打印服务器和每个服务器安装的打印机的网页。 可以通过这些页面中的链接引用其他页面。

对于支持网页的 Windows 2000 打印服务器，该服务器必须运行带有 Microsoft Internet Information Server (IIS) 或 Windows 2000 Professional software with Microsoft 对等 Web 服务器的 Windows 2000 服务器软件。

为了使 Windows XP 打印服务器支持网页，它必须运行 Microsoft Windows Server 2003 software with Microsoft Internet Information Server (IIS) 或 Windows XP Professional software with Microsoft 对等 Web 服务器。 请注意，Windows XP Home Edition 中的打印服务器不支持网页。

若要查看打印服务器页面，用户需要指定以下 URL 格式：

https:// &lt; ServerName &gt; /printers

其中 &lt; ServerName &gt; 是服务器名称 (Internet 连接的 DNS 名称或 intranet 连接的 WINS 名称) 。 URL 指向用于生成打印服务器页面的 HTML 文件。

服务器页为服务器上提供的每个打印队列提供了一个指向打印队列页面的链接。 所有用户都可以访问共享打印队列。 用户还可以通过使用以下格式指定 URL 来引用共享打印机的打印队列页面：

https:// &lt; ServerName &gt; / &lt; 共享名&gt;

其中， &lt; 共享 &gt; 名是打印队列的共享名，在其属性表中指定。

如果用户在打印文件夹中选择打印机的链接，则将自动启动 Windows Internet Explorer 并访问打印队列页的 URL。 或者，正如前面所述，用户可以通过指定页面的 URL 来查看 "打印服务器" 页或 "打印队列" 页。

打印网页是从可由 Microsoft Active Server Pages (ASP) 解释的模板文件生成的。 这些模板 (称为 ASP 文件) 包含标准 HTML 标记和 (&lt; % 和%) 的 asp 脚本标记 &gt; 。

当 Active Server Pages 解释器在 ASP script 标记中遇到文本时，它会调用相应的脚本语言解释器 (如 JScript 或 VBScript) 来处理文本。 然后，将生成的 HTML 数据流发送到客户端浏览器。

有关 Microsoft Active Server 页面的详细信息，请参阅 Microsoft Windows SDK 文档。

提供了一组基于 COM 的 [ActiveX 对象](activex-objects-for-print-web-pages.md)，其中包含关联的自动化界面，可在 Oleprn.dll) 中 (，以获取打印机属性和 SNMP 信息。

当用户想要查看特定服务器或打印机的网页时，将执行以下步骤：

1.  用户使用浏览器指定适当的 URL。 该 URL 指向指定打印服务器上的一个模板文件。

2.  服务器驻留的 Active Server Pages 解释器是 IIS 的一部分，搜索 ASP 脚本标记，调用相应的脚本语言解释器来解释脚本文本，并将返回的结果放入 HTML 数据流。

3.  服务器上的 ASP 解释器将生成的 HTML 流发送到客户端的浏览器。

下图说明了将打印机 URL 从客户端发送到打印服务器的过程，以及如何将其关联的 HTML 流返回到客户端。

![说明如何将打印 url 从客户端发送到打印服务器的关系图](images/prnturl.png)

 

 




