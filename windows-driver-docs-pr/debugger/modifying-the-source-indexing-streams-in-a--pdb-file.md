---
title: 修改源索引中的.pdb 文件的流
description: 修改源索引中的.pdb 文件的流
ms.assetid: 9c319667-fc71-4baf-ad12-a20e18b67d40
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d82119e1214b6c09f4017d0586c2d77b0d4ea938
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526819"
---
# <a name="modifying-the-source-indexing-streams-in-a-pdb-file"></a>修改源索引中的.pdb 文件的流


对于使用 SrcSrv 网站调试器客户端，必须修改.pdb 文件以指向它。 若要手动执行此操作，使所有.pdb 文件的副本，更改它们，并将它们从单独的位置-通常该网站本身提供。

调试工具的 Windows 提供了三个文件，以帮助在重新配置的.pdb 文件。 Cv2http.cmd 和 Cv2http.pl 文件提取 SrcSrv 数据流对该、 使用 Perl 脚本中，修改它和将更改后的流放回的.pdb 文件。 语法是按如下所示：

```console
cv2http.cmd PDB Alias URL
```

其中*PDB*指定名称的修改，.pdbfile*别名*指定的逻辑名称，若要将应用于您的网站，并*URL*指定站点的完整 URL。 请注意，*别名*参数存储在 PDB 中为调试器客户端在 Scrsrv.ini，可以重写的变量名称应不断移动的网站的位置。

此脚本需要所有标准 SrcSrv 工具是在路径中可用，因为它会调用 SrcTool 和 PDBStr。 请记住 Cv2http.pl 是 Perl 脚本，可以修改以满足你的需求。

第三个文件，遍历 (walk.cmd) 脚本中，修改一整个组的.pdb 文件。 例如：

```console
walk.cmd *.pdb cv2http.cmd HttpAlias https:///source
```

上述命令对每个.pdb 文件在树中，为该别名使用 HttpAlias 调用 Cv2http.cmd 和 https://server/source的 url。 有关审核的更多详细信息，请参阅[提取源文件](extracting-source-files.md)。

在树的.pdb 文件上执行此命令后，他们就可以安装在网站或要在其中任何的位置将其放到。 请记住，可以使用 SrcTool 和 PDBStr 若要检查的.pdb 文件的更改。

 

 





