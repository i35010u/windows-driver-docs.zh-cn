---
title: SrcTool 实用工具
description: SrcTool 实用工具
keywords:
- Srcsrv.ini，Srctool.exe 实用工具
- Srctool.exe 实用程序
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ea98198d553b30118dd4a9a4aa007d53c96a173
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841141"
---
# <a name="the-srctool-utility"></a>SrcTool 实用工具


Srctool.exe ( # A0) 实用工具列出了在 .pdb 文件中编制索引的所有文件。 对于每个文件，它将列出文件的完整路径、源代码管理服务器和版本号。 您可以使用此信息来参考。

还可以使用 Srctool.exe 列出 .pdb 文件中的原始源文件信息。 为此，请在命令行上使用 **-s** 开关。

Srctool.exe 还具有其他选项。 使用 **？** 切换以查看它们。 最重要的是，此实用工具可用于从版本控制中提取所有源文件。 这是通过 **-x** 开关来完成的。

**注意**   此程序的以前版本在提取文件时，创建了一个名为 src 下的目录。 这种情况不会再出现。 如果希望使用 src 目录，则必须自行创建该目录，并从该目录运行该命令。

 

 

 





