---
title: SrcTool 实用工具
description: SrcTool 实用工具
ms.assetid: d8669a91-4361-41d6-a7ba-a6d1a706ff66
keywords:
- SrcSrv，SrcTool 实用工具
- SrcTool 实用工具
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4806687df618466f0faa28602f007f15ca55f98
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566090"
---
# <a name="the-srctool-utility"></a>SrcTool 实用工具


SrcTool (Srctool.exe) 实用程序列出在.pdb 文件编制索引的所有文件。 对于每个文件，它列出的完整路径、 源代码管理服务器和文件的版本号。 例如，可以使用此信息。

您还可以使用 SrcTool 列出从.pdb 文件的原始源文件信息。 若要执行此操作，请使用 **-s**开关在命令行上。

SrcTool 已以及其他选项。 使用 **？** 若要查看这些开关。 最受关注的是此实用工具可用于从版本控制中提取所有源代码文件。 这通过 **-x**切换。

**请注意**  此程序的早期版本创建名为当前目录下方的 src 提取文件时的目录。 这不再是这种情况。 如果你想使用的 src 目录，必须自行创建它，并从该目录运行该命令。

 

 

 





