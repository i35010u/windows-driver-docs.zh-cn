---
title: 使用 CDB 打开转储文件
description: 使用 CDB 打开转储文件
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72cb8711be9d103a4e69253c54e3a822d38bbd5b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833629"
---
# <a name="opening-a-dump-file-using-cdb"></a>使用 CDB 打开转储文件


## <a name="span-idcommand_promptspanspan-idcommand_promptspanspan-idcommand_promptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符


在命令提示符窗口中，您可以在启动 CDB 时打开用户模式转储文件。 输入以下命令。

**cdb-y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V** 选项 (详细模式) 也很有用。 有关命令行语法的详细信息，请参阅 [ **CDB Command-Line 选项**](cdb-command-line-options.md)

## <a name="span-idcdb_command_linespanspan-idcdb_command_linespanspan-idcdb_command_linespancdb-command-line"></a><span id="CDB_Command_Line"></span><span id="cdb_command_line"></span><span id="CDB_COMMAND_LINE"></span>CDB 命令行


您还可以通过输入 [**opendump (打开转储文件)**](-opendump--open-dump-file-.md) 命令，然后按 [**g (中转)**](g--go-.md)，在调试器运行后打开转储文件。 这允许同时调试多个转储文件。

 

 





