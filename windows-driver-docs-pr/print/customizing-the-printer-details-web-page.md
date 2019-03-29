---
title: 自定义打印机详细信息网页
description: 自定义打印机详细信息网页
ms.assetid: 4853d5de-b855-4698-9178-877455e257c5
keywords:
- 自定义打印网页 WDK，创建页
- ASP 文件 WDK 打印机
- 端口监视 WDK 打印、 自定义 Web 页
- 自定义打印网页 WDK，详细信息页
- 详细信息页上的 WDK 打印机
- 打印网页 WDK，详细信息页
- 网页 WDK 打印机，详细信息页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b22da2904aa30f44c33762c7b4db1562deb623b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569338"
---
# <a name="customizing-the-printer-details-web-page"></a>自定义打印机详细信息网页

如果你想要替换由 Microsoft 提供的打印机详细信息页，可以提供一个或多个自定义的 ASP 文件。 如果您替换默认页面，您还可以提供在服务器上安装的其他自定义页面的链接以及在 Web 上找到的任何其他页面的链接。

如果 Microsoft 的标准 TCP/IP[端口监视器](https://docs.microsoft.com/windows-hardware/drivers/print/port-monitors)与打印机一起使用 (Tcpmon.dll)，可以使用自定义的 ASP 文件来替换默认打印机的详细信息页上的每个打印机类型或每个制造商基础。 如果尚未安装自定义的 ASP 文件，则使用默认打印机的详细信息页。

自定义的 ASP 文件还可用于替换为使用其他端口监视器，但每个打印机类型的打印机的默认打印机的详细信息页并不允许每个制造商替换内容。

用于安装自定义的 ASP 文件的方法确定是否将自定义的文件替换为打印机类型、 制造商或端口监视器的默认文件。 有关详细信息，请参阅[安装自定义打印网页](installing-customized-print-web-pages.md)。

以下主题提供有关创建打印网页的详细信息：

[替换为默认打印机的详细信息页](replacing-the-default-printer-details-page.md)

[将显示哪些打印机的详细信息页？](which-printer-details-page-is-displayed-.md)

[打印网页的 ASP 变量](asp-variables-for-print-web-pages.md)

[打印网页的 ActiveX 对象](activex-objects-for-print-web-pages.md)

[更新 Web 页面信息](updating-web-page-information.md)
