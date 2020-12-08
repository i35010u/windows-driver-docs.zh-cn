---
title: 替换默认的打印机详细信息页
description: 替换默认的打印机详细信息页
keywords:
- 自定义的打印网页 WDK，替换默认页面
- 替换默认打印机详细信息页
- 默认打印机详细信息页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5291765f445f2b23eb9d6ae880fce57579eb5559
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807033"
---
# <a name="replacing-the-default-printer-details-page"></a>替换默认的打印机详细信息页





您可以使用以下步骤将默认打印机详细信息页替换为自定义页面：

1.  为页面提供自定义的 ASP 文件。

2.  按照 [安装自定义的打印网页](installing-customized-print-web-pages.md)中所述的安装过程进行操作。

自定义的打印机详细信息页可以提供指向其他自定义页或任何其他 Url 的链接。 必须按照 [安装自定义的打印网页](installing-customized-print-web-pages.md)中的说明安装其他自定义页面的 ASP 文件。 有关指定链接的信息，请参阅 Microsoft Windows SDK 文档中的 ASP 文档。

自定义的打印网页可以使用以下技术：

[打印网页的 ASP 变量](asp-variables-for-print-web-pages.md)

[打印网页的 ActiveX 对象](activex-objects-for-print-web-pages.md)

自定义 COM 对象

有关创建和使用 COM 对象的信息，请参阅 Windows SDK 文档。

**注意**   使用 ASP 文件创建的所有打印网页都是从单个 ASP 应用程序生成的。
不得修改名为 Globals 的文件，该文件包含在系统磁盘的 "打印机" 子目录中。

Microsoft 保留在不另行通知的情况下修改其打印网页的权限。 因此，自定义的 ASP 文件不得依赖于 Microsoft 提供的 ASP 文件的内容。

 

 

 




