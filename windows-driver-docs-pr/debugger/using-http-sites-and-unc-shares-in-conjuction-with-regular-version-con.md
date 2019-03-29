---
title: 结合常规版本控制使用 HTTP 站点和 UNC 共享
description: 结合常规版本控制使用 HTTP 站点和 UNC 共享
ms.assetid: 1b045a00-45e7-47e8-9447-7d94f70253fe
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0332d15c5fc349d86c63882fa5e84a4a90d8ef63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576087"
---
# <a name="using-http-sites-and-unc-shares-in-conjuction-with-regular-version-control"></a>结合常规版本控制使用 HTTP 站点和 UNC 共享


您可能会发现，必须支持您的开发人员使用的标准 SrcSrv 功能，从版本控制中提取文件，但还必须使源文件可通过网站或 UNC 共享。 如果已经设置了测试实验室不能访问到版本控制的则可能发生这种情况。 它是可以支持这两个用户使用同一组.pdb 文件。

首先，提取使用 SrcTool; 在源代码文件请参阅[提取源文件](extracting-source-files.md)有关详细信息。 使该共享可为网站或 UNC 共享。 对于当前目的，你不应转换使用 Cv2http.cmd 脚本的.pdb 文件。

现在将使用 HTTP/UNC 共享的计算机，在编辑[Srcsrv.ini](the-srcsrv-ini-file.md)调试器目录中的文件。 在文件的变量部分中，添加以下三个语句：

```ini
MY_SOURCE_ROOT=\\server\share
 SRCSRVCMD=
 SRCSRVTRG=%MY_SOURCE_ROOT%\%var2%\%var3%\%var4%\%fnfile%(%var1%)
```

应替换\\ \\server\\共享与你要提供的 UNC 共享的根目录或包含源文件的网站的 URL。 您还可以更改 MY\_源\_根是您想要描述此位置的任何别名。 这些例外情况之外，其他所有内容应输入严格按照所述。

在这种方式中设置的所有调试器忽略标准版本控制的提取指令，并改为从指定的位置访问源文件。 同时，而无需在 Srcsrv.ini 中包含这些项的所有调试器都使用正常的版本控制机制来提取源文件。

 

 





