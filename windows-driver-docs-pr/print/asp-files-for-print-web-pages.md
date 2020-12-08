---
title: 打印网页的 ASP 文件
description: 打印网页的 ASP 文件
keywords:
- 自定义的打印网页 WDK、ASP 文件
- ASP 文件 WDK 打印机
- 打印网页 WDK，ASP 文件
- 网页 WDK 打印机，ASP 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 504f467b05bb58b956a30f3ab0fc0d17b464d3b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836153"
---
# <a name="asp-files-for-print-web-pages"></a>打印网页的 ASP 文件





打印网页是使用 ASP 文件创建的。 Microsoft 提供了创建以下打印网页的 ASP 文件：

- URL https://<em> &lt; servername &gt;</em>/printers 引用的打印服务器页面，其中 *&lt; ServerName &gt;* 代表打印服务器的 DNS 或 WINS 名称。 此页包含指向服务器上安装的每个打印机的页面的链接。

- 每个服务器的打印队列的打印队列页。 可以通过 "打印服务器" 页中的链接访问这些页，也可以使用 URL https://<em> &lt; ServerName &gt;</em> / *&lt; 共享 &gt;* 项直接从浏览器引用这些页。

- 排队文档的其他页、打印机属性和打印机特定的详细信息。 这些页面显示在 "打印队列" 页的帧中。

可以通过替换其 ASP 文件来自定义打印机特定的详细信息页。 有关详细信息，请参阅 [自定义打印机详细信息](customizing-the-printer-details-web-page.md)网页。

 

 




