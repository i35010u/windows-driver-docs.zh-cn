---
title: 源索引
description: 源索引
keywords:
- 源索引
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c305447ab590865f86cf915e3cefd26a23c57ebd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791623"
---
# <a name="source-indexing"></a>源索引


通常，生成应用程序后，会在生成过程中对二进制文件进行源索引。 Srcsrv.ini 所需的信息存储在 .pdb 文件中。 Srcsrv.ini 目前支持以下源代码管理系统：

-   Perforce

-   Microsoft Visual SourceSafe

-   Microsoft Team Foundation Server

还可以创建自定义脚本，为不同的源代码管理系统创建代码索引。 此包中包含一个此类用于 Subversion 的模块。

Srcsrv.ini 包括五个在源索引过程中使用的工具：

[Srcsrv.ini 文件](the-srcsrv-ini-file.md)

[Ssindex.cmd 脚本](the-ssindex-cmd-script.md)

[SrcTool 实用工具](the-srctool-utility.md)

[PDBStr 工具](the-pdbstr-tool.md)

[VSSDump 工具](the-vssdump-tool.md)

这些工具随用于 Windows 的调试工具安装在 srcsrv.ini 子目录中，应保持安装在与 Srcsrv.ini 相同的路径中。 这些工具中的 PERL 脚本需要 PERL 5.6 或更高版本。

 

 





