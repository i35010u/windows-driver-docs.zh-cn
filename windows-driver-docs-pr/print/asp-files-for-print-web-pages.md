---
title: 打印网页的 ASP 文件
description: 打印网页的 ASP 文件
ms.assetid: 01ca39ed-be16-41fb-b432-1cbd0908358d
keywords:
- 自定义打印网页 WDK、 ASP 文件
- ASP 文件 WDK 打印机
- 打印网页 WDK、 ASP 文件
- 网页 WDK 打印机，ASP 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 842227883a534b96507975e210f077872a904ec2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363245"
---
# <a name="asp-files-for-print-web-pages"></a>打印网页的 ASP 文件





打印网页使用创建的 ASP 文件。 Microsoft 提供了创建以下的 ASP 文件打印网页：

- 打印服务器页上的引用的 URL http://<em>&lt;ServerName&gt;</em>/printers，其中 *&lt;ServerName&gt;* 表示 DNS 或 WINS打印服务器的名称。 此页包含用于在服务器上安装每个打印机的页面的链接。

- 用于每个服务器的打印队列的打印队列页面。 可通过打印服务器页中的链接访问这些页面也可以直接从浏览器中使用 URL http:// 中引用<em>&lt;ServerName&gt;</em>  /  *&lt;ShareName&gt;* 。

- 队列的文档、 打印机属性和特定于打印机的详细信息的其他页。 这些页面的打印队列页范围内显示。

可以通过将其 ASP 文件替换为自定义特定于打印机的详细信息页。 有关详细信息，请参阅[自定义打印机的详细信息网页](customizing-the-printer-details-web-page.md)。

 

 




