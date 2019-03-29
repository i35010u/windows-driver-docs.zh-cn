---
title: 源索引
description: 源索引
ms.assetid: 381020c6-26b1-48ab-bc7d-9ab718ecb89f
keywords:
- 源索引编制
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b418ffcee52752657ba98ee3cc94b67f375ab63
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563209"
---
# <a name="source-indexing"></a>源索引


通常情况下，二进制文件包括编制源索引在生成过程后生成应用程序。 SrcSrv 所需的信息存储在.pdb 文件。 SrcSrv 目前支持以下源控制系统：

-   Perforce

-   Microsoft Visual SourceSafe

-   Microsoft Team Foundation Server

此外可以创建自定义脚本，用于不同的源控制系统代码的索引。 此包中包含的 Subversion 这样一个模块。

SrcSrv 包含源索引编制过程中使用的五个工具：

[Srcsrv.ini 文件](the-srcsrv-ini-file.md)

[Ssindex.cmd 脚本](the-ssindex-cmd-script.md)

[SrcTool 实用工具](the-srctool-utility.md)

[PDBStr 工具](the-pdbstr-tool.md)

[VSSDump 工具](the-vssdump-tool.md)

这些工具中安装了有关 Windows 调试工具与子目录 srcsrv，以及应保留已安装在与 SrcSrv 相同的路径。 在这些工具在 PERL 脚本需要 PERL 5.6 或更高版本。

 

 





