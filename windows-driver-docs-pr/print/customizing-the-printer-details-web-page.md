---
title: 自定义打印机详细信息网页
description: 自定义打印机详细信息网页
keywords:
- 自定义的打印网页 WDK，创建页面
- ASP 文件 WDK 打印机
- 端口监视 WDK 打印，自定义网页
- 自定义的打印网页 WDK，详细信息页
- 详细信息页 WDK 打印机
- 打印网页 WDK，详细信息页
- 网页 WDK 打印机，详细信息页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f80abaf9d687f2e4c726fb0587a0f3484e8d55d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797365"
---
# <a name="customizing-the-printer-details-web-page"></a>自定义打印机详细信息网页

如果要替换 Microsoft 提供的 "打印机详细信息" 页，则可以提供一个或多个自定义 ASP 文件。 如果替换默认页面，还可以提供指向安装在服务器上的其他自定义页面的链接，以及指向 Web 上任何其他页面的链接。

如果将 Microsoft 的标准 TCP/IP [端口监视器](./port-monitors.md) ( # A0) 与打印机一起使用，则可以使用自定义的 ASP 文件，根据打印机类型或每个制造商替换默认打印机详细信息页。 如果尚未安装自定义的 ASP 文件，则使用默认的打印机详细信息页。

自定义的 ASP 文件还可用于使用其他端口监视器替换打印机的默认打印机详细信息页，但不允许使用每个打印机类型和每个制造商的替换项。

用于安装自定义 ASP 文件的方法确定自定义文件是否替换打印机类型、制造商或端口监视器的默认文件。 有关详细信息，请参阅 [安装自定义的打印网页](installing-customized-print-web-pages.md)。

以下主题提供了有关创建打印网页的详细信息：

[替换默认的打印机详细信息页](replacing-the-default-printer-details-page.md)

[显示哪个打印机详细信息页？](which-printer-details-page-is-displayed-.md)

[打印网页的 ASP 变量](asp-variables-for-print-web-pages.md)

[打印网页的 ActiveX 对象](activex-objects-for-print-web-pages.md)

[更新网页信息](updating-web-page-information.md)
