---
title: Ssindex.cmd 脚本
description: Ssindex.cmd 脚本
keywords:
- Srcsrv.ini，Ssindex.cmd 脚本
- Ssindex.cmd 脚本
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c6b7144cedab6b48b4516633698c3a4c771a63c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813895"
---
# <a name="the-ssindexcmd-script"></a>Ssindex.cmd 脚本


Ssindex.cmd 脚本生成签入源代码管理的文件列表以及每个文件的版本信息。 它在生成应用程序时生成的 .pdb 文件中存储此信息的子集。 Ssindex.cmd 使用以下 Perl 模块之一与源控件交互：

-   p4.pm (Perforce) 

-   vss.pm (Visual SourceSafe) 

-   tfs.pm (Team Foundation Server) 

-   svn.pm (Subversion) 

有关详细信息，请运行包含 **-？** 的 ssindex.cmd 或 **-??**  (详细帮助) 选项或检查脚本。

 

 





