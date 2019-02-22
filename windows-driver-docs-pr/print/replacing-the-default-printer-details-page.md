---
title: 替换为默认打印机的详细信息页
description: 替换为默认打印机的详细信息页
ms.assetid: 451f442b-a882-4540-82dd-e96dab5e7619
keywords:
- 自定义打印网页 WDK，替换默认页
- 替换为默认打印机的详细信息页
- 默认打印机的详细信息页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fa10d88c203be24a246eb7937bc1a0bad70308cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524193"
---
# <a name="replacing-the-default-printer-details-page"></a>替换为默认打印机的详细信息页





通过使用以下步骤，可以使用自定义页面替换默认打印机的详细信息页：

1.  提供自定义的 ASP 文件的页。

2.  按照中所述的安装步骤[安装自定义打印网页](installing-customized-print-web-pages.md)。

自定义的打印机的详细信息页可以提供其他自定义页面的链接或任何其他 Url。 必须安装其他自定义页面的 ASP 文件，如下所示[安装自定义打印网页](installing-customized-print-web-pages.md)。 有关指定链接的信息，请参阅 Microsoft Windows SDK 文档中的 ASP 文档。

自定义打印网页可以使用以下技术：

[打印网页的 ASP 变量](asp-variables-for-print-web-pages.md)

[打印网页的 ActiveX 对象](activex-objects-for-print-web-pages.md)

自定义的 COM 对象

有关创建和使用 COM 对象的信息，请参阅 Windows SDK 文档。

**请注意**  从单个 ASP 应用程序生成的所有使用 ASP 文件创建的打印网页。
必须修改名为 Globals.asp，系统磁盘的打印机子目录中包含的文件。

Microsoft 保留权修改恕不另行通知的打印网页。 因此，自定义的 ASP 文件必须不依赖于 Microsoft 提供的 ASP 文件的内容。

 

 

 




