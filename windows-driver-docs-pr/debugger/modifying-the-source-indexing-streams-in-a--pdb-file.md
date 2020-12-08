---
title: 修改 .pdb 文件中的源索引流
description: 修改 .pdb 文件中的源索引流
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4019dbde53bfb1931e3e59dbeb5f12fc5a2bba2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798369"
---
# <a name="modifying-the-source-indexing-streams-in-a-pdb-file"></a>修改 .pdb 文件中的源索引流


要使调试器客户端使用 Srcsrv.ini 网站，必须将 .pdb 文件修改为指向该文件。 若要手动执行此操作，请创建所有 .pdb 文件的副本，对其进行更改，并使其在单独的位置（通常为网站本身）中可用。

适用于 Windows 的调试工具提供了三个文件以帮助重新配置 .pdb 文件。 Cv2http 和 Cv2http.pl 文件提取 Srcsrv.ini 流，使用 Perl 脚本对其进行修改，并将更改后的流放回 .pdb 文件中。 语法如下：

```console
cv2http.cmd PDB Alias URL
```

其中 *PDB* 指定要修改的 pdbfile 的名称， *Alias* 指定要应用于您的网站的逻辑名称， *URL* 指定该站点的完整 URL。 请注意， *Alias* 参数在 PDB 中存储为可在 Scrsrv.ini 中的调试器客户端上重写的变量名，因此，您是否应该移动网站的位置。

此脚本要求在路径中提供所有标准 Srcsrv.ini 工具，因为它同时调用 Srctool.exe 和 Pdbstr.exe。 请记住，Cv2http.pl 是 Perl 脚本，可以修改以满足你的需求。

第三个文件（行走 (行走 .cmd) 脚本）修改一组完整的 .pdb 文件。 例如：

```console
walk.cmd *.pdb cv2http.cmd HttpAlias https:///source
```

上述命令在树中的每个 .pdb 文件上调用 Cv2http，并将 HttpAlias 用于别名和 https://server/source URL。 有关浏览的详细信息，请参阅 [提取源文件](extracting-source-files.md)。

在 .pdb 文件树中执行此命令后，它们就可以安装到网站中，也可以安装在任何要放置它们的位置。 请记住，您可以使用 Srctool.exe 和 Pdbstr.exe 来检查对 .pdb 文件的更改。

 

 





