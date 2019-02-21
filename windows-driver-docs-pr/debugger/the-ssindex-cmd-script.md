---
title: Ssindex.cmd 脚本
description: Ssindex.cmd 脚本
ms.assetid: 38bff31a-af4e-4fd4-bdf6-da901067bdd0
keywords:
- SrcSrv，Ssindex.cmd 脚本
- Ssindex.cmd 脚本
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6919455b6405bee51d73913f3d8842845defa6c9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547736"
---
# <a name="the-ssindexcmd-script"></a>Ssindex.cmd 脚本


Ssindex.cmd 脚本将生成的文件签入源代码管理，以及每个文件的版本信息的列表。 它在生成时生成了应用程序的.pdb 文件中存储此信息的子集。 SSIndex 使用以下的 Perl 模块之一以便与源代码管理：

-   p4.pm (Perforce)

-   vss.pm (Visual SourceSafe)

-   tfs.pm (Team Foundation Server)

-   svn.pm (Subversion)

有关详细信息，运行使用 Ssindex.cmd **-？** 或 **-??** （详细的帮助） 选项，或检查脚本。

 

 





