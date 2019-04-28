---
title: 使用 CDB 打开转储文件
description: 使用 CDB 打开转储文件
ms.assetid: 204DFA6F-2BA2-4B76-AFE0-28207710322B
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d7bcc014ca2c85e294c2edc19a669d3ad175c40
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63354895"
---
# <a name="opening-a-dump-file-using-cdb"></a>使用 CDB 打开转储文件


## <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符


在命令提示符窗口中，可以打开用户模式转储文件，则在启动 CDB 时。 输入以下命令。

**cdb -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 （详细模式） 也是很有用。 有关命令行语法的详细信息，请参阅[ **CDB 命令行选项**](cdb-command-line-options.md)

## <a name="span-idcdbcommandlinespanspan-idcdbcommandlinespanspan-idcdbcommandlinespancdb-command-line"></a><span id="CDB_Command_Line"></span><span id="cdb_command_line"></span><span id="CDB_COMMAND_LINE"></span>CDB 命令行


通过输入运行调试器后，还可以打开转储文件[ **.opendump （打开转储文件）** ](-opendump--open-dump-file-.md)命令后, 跟[ **g （转向）** ](g--go-.md). 这样，您可以同时调试多个转储文件。

 

 





