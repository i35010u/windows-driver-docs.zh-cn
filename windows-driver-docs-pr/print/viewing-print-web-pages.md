---
title: 查看打印网页
description: 查看打印网页
ms.assetid: c2cf782c-0f53-47e1-8c5e-1e2aa87613c4
keywords:
- Internet 打印 WDK，并查看打印网页
- 查看打印网页
- 显示打印网页
- 打印网页 WDK 中查看
- 网页 WDK 打印机、 查看
- WDK 中的打印服务器页
- 查看打印服务器页
- 打印 Url WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 706b189efd5834df0f3246d32407ff65de6b8292
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345286"
---
# <a name="viewing-print-web-pages"></a>查看打印网页





与任何类型的客户端平台上执行任何 Internet 浏览器中，用户可以查看网页的显示状态的 Microsoft Windows 2000 或更高版本打印服务器和其连接的打印机。 Microsoft 提供了一组-驻留在服务器上生成这些网页的 HTML 文件。 使用 Url 的客户端浏览器，可以引用网页打印服务器和每个服务器安装打印机。 从这些页面的链接，可以引用其他页。

对于以支持 Web 页的 Windows 2000 打印服务器，它必须运行任一 Windows 2000 Server 的软件与 Microsoft Internet 信息服务器 (IIS) 或与 Microsoft 对等 Web 服务器的 Windows 2000 Professional 软件。

为了使 Windows XP 的打印服务器能支持 Web 页面，它必须运行任一 Microsoft Windows Server 2003 的软件与 Microsoft Internet 信息服务器 (IIS) 或与 Microsoft 对等 Web 服务器的 Windows XP Professional 软件。 请注意，在 Windows XP Home Edition 中的打印服务器不支持 Web 页。

若要查看打印服务器页上，用户指定以下 URL 格式：

http://&lt;ServerName&gt;/printers

其中&lt;ServerName&gt;是服务器名称 （Internet 连接的 DNS 名称），或者 intranet 连接的 WINS 名称。 该 URL 指向生成的打印服务器的页面的 HTML 文件。

服务器页提供了为每个服务器上可用的打印队列的打印队列页面的链接。 可以通过所有用户访问共享的打印队列。 用户还可以通过使用以下格式指定 URL 引用的共享打印机的打印队列页：

http://&lt;ServerName&gt;/&lt;ShareName&gt;

其中&lt;ShareName&gt;是打印队列的共享名称，其属性表中指定。

如果用户选择打印机的打印文件夹中的链接，自动启动 Windows Internet Explorer 并访问打印队列页面的 URL。 或者，如前面所述，用户可以查看打印服务器页面或打印队列页面通过指定的任何 HTML 浏览器的页面的 URL。

从可以解释通过 Microsoft Active Server Pages (ASP) 的模板文件生成打印网页。 这些模板 （称为 ASP 文件） 包含标准的 HTML 标记和 ASP 脚本标记 (&lt;%和 %&gt;)。

当 Active Server Pages 解释器遇到 ASP 脚本标记中的文本时，它将调用相应脚本语言解释器 （如 JScript 或 VBScript） 以处理文本。 生成的 HTML 数据流然后发送到客户端浏览器。

有关 Microsoft Active Server Pages 的详细信息，请参阅 Microsoft Windows SDK 文档。

基于 COM 的一套[打印网页的 ActiveX 对象](activex-objects-for-print-web-pages.md)，与关联的自动化界面，用于获取打印机属性和 SNMP 信息提供 （在 Oleprn.dll)。

当用户想要查看特定服务器或打印机的 Web 页面时，将执行以下步骤：

1.  用户使用浏览器来指定适当的 URL。 URL 指向一个指定的打印服务器上的模板文件。

2.  驻留在服务器中的 Active Server Pages 解释程序，它是 IIS 的一部分，搜索 ASP 脚本标记，调用相应脚本语言解释器解释脚本文本，并将返回的结果放置在 HTML 数据流。

3.  ASP 解释器，在服务器上，将生成的 HTML 流发送到客户端浏览器。

下图说明了按其打印机 URL 从客户端发送到打印服务器，以及如何将其关联的 HTML 流返回到客户端的过程。

![说明将打印 url 从客户端发送到打印服务器的关系图](images/prnturl.png)

 

 




