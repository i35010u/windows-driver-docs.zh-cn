---
title: 结合常规版本控制使用 HTTP 站点和 UNC 共享
description: 结合常规版本控制使用 HTTP 站点和 UNC 共享
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91b82704ccb4ea44451311191d8cf4c8f5aa2185
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803106"
---
# <a name="using-http-sites-and-unc-shares-in-conjuction-with-regular-version-control"></a>结合常规版本控制使用 HTTP 站点和 UNC 共享


你可能会发现，你必须支持开发人员使用标准的 Srcsrv.ini 功能，该功能可从版本控制中提取文件，但还必须通过网站或 UNC 共享来提供源文件。 如果您设置了一个无法访问版本控制的测试实验室，则可能会发生这种情况。 可以使用同一组 .pdb 文件来支持这两个用户。

首先，使用 Srctool.exe 提取源文件;有关详细信息，请参阅 [提取源文件](extracting-source-files.md) 。 将共享作为网站或 UNC 共享提供。 对于当前目的，不应使用 Cv2http 脚本转换 .pdb 文件。

现在，在将使用 HTTP/UNC 共享的计算机上，编辑调试器目录中的 [Srcsrv.ini](the-srcsrv-ini-file.md) 文件。 在该文件的 variables 节中，添加以下三个语句：

```ini
MY_SOURCE_ROOT=\\server\share
 SRCSRVCMD=
 SRCSRVTRG=%MY_SOURCE_ROOT%\%var2%\%var3%\%var4%\%fnfile%(%var1%)
```

应将 \\ \\ 服务器共享替换为 \\ 您提供的 UNC 共享的根目录或包含源文件的网站的 URL。 你还可以将 \_ 源 \_ 根目录更改为你要描述此位置的任何别名。 有了这些例外，应严格按照所述输入所有其他内容。

以这种方式设置的所有调试器都将忽略标准版本控制提取说明，并改为从指定的位置访问源文件。 同时，Srcsrv.ini 中不包含这些项的所有调试器都使用常规版本控制机制来提取源文件。

 

 





