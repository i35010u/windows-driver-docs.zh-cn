---
title: 使用 UNC 共享
description: 使用 UNC 共享
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1165d10bc9478c016abbf5c62a9d5f9dc7393a80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802997"
---
# <a name="using-unc-shares"></a>使用 UNC 共享


Cv2http、Cv2http.pl 和行走 (行走) 脚本用于提供简单 UNC 共享中的源文件。 文件 Cv2http 和 Cv2http.pl 提取 Srcsrv.ini 流，使用 Perl 脚本对其进行修改，并将更改后的流放回 .pdb 文件中。 语法如下：

`cv2http.cmd PDB Alias SourceRoot`

其中 *PDB* 指定要修改的 pdbfile 的名称， *Alias* 指定要应用于您的网站的逻辑名称，而 *SourceRoot* 指定您将源文件提取到的 UNC 共享的根目录。 请注意， *Alias* 参数在 PDB 中存储为变量名称，可以在 Scrsrv.ini 中的调试器客户端上重写该名称，而您是否要移动网站的位置。

此脚本要求在路径中提供所有标准 Srcsrv.ini 工具，因为它同时调用 Srctool.exe 和 Pdbstr.exe。 请记住，Cv2http.pl 是 Perl 脚本，可以修改以满足你的需求。

第三个文件（行走 (行走 .cmd) 脚本）修改一组完整的 .pdb 文件。 例如：

```console
walk.cmd *.pdb cv2http.cmd SourceRoot \\server\share
```

上述命令在树中的每个 .pdb 文件上调用 Cv2http，并使用 SourceRoot 作为 UNC 共享的别名和 \\ \\ 服务器 \\ 共享。 有关浏览的详细信息，请参阅 [提取源文件](extracting-source-files.md)。

在 .pdb 文件树中执行此命令后，它们就可以安装到网站中，也可以安装在任何要放置它们的位置。 请记住，您可以使用 Srctool.exe 和 Pdbstr.exe 来检查对 .pdb 文件的更改。

 

 





