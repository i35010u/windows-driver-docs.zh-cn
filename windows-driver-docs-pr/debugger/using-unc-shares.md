---
title: 使用 UNC 共享
description: 使用 UNC 共享
ms.assetid: 7baf157d-e8c3-4ad5-a56e-58f8983da4d9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1621fd19ba2a159becf52babce7c7b87bac5b617
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521215"
---
# <a name="using-unc-shares"></a>使用 UNC 共享


Cv2http.cmd、 Cv2http.pl 和遍历 (Walk.cmd) 脚本用于提供简单的 UNC 共享中的源文件。 文件 Cv2http.cmd 和 Cv2http.pl 提取 SrcSrv 数据流对该、 使用 Perl 脚本中，修改它和将更改后的流放回的.pdb 文件。 语法是按如下所示：

`cv2http.cmd PDB Alias SourceRoot`

其中*PDB*指定名称的修改，.pdbfile*别名*指定的逻辑名称，若要将应用于您的网站，并*SourceRoot*指定的 UNC 共享的根提取到的源文件。 请注意，*别名*参数存储在 PDB 中为调试器客户端在 Scrsrv.ini，可以重写的变量名称应不断移动的网站的位置。

此脚本需要所有标准 SrcSrv 工具是在路径中可用，因为它会调用 SrcTool 和 PDBStr。 请记住 Cv2http.pl 是 Perl 脚本，可以修改以满足你的需求。

第三个文件，遍历 (walk.cmd) 脚本中，修改一整个组的.pdb 文件。 例如：

```console
walk.cmd *.pdb cv2http.cmd SourceRoot \\server\share
```

上述命令对每个.pdb 文件在树中，为该别名使用 SourceRoot 调用 Cv2http.cmd 并\\ \\server\\共享的 UNC 共享。 有关审核的更多详细信息，请参阅[提取源文件](extracting-source-files.md)。

在树的.pdb 文件上执行此命令后，他们就可以安装在网站或要在其中任何的位置将其放到。 请记住，可以使用 SrcTool 和 PDBStr 若要检查的.pdb 文件的更改。

 

 





