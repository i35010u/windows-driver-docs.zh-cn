---
title: 使用 KD 打开转储文件
description: 使用 KD 打开转储文件
ms.assetid: 458E9BA6-6FA0-4FEF-93A0-062C9E11D21F
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcca62c84df3552034f3240a783ca4e7a10e977d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385039"
---
# <a name="opening-a-dump-file-using-kd"></a>使用 KD 打开转储文件


## <a name="span-idcommandpromptspanspan-idcommandpromptspanspan-idcommandpromptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符


在命令提示符窗口中，可以打开转储文件，则在启动 KD 时。 使用以下命令。

**kd -y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V**选项 （详细模式） 也是很有用。 有关命令行语法的详细信息，请参阅[ **KD 命令行选项**](kd-command-line-options.md)。

## <a name="span-idkdcommandlinespanspan-idkdcommandlinespanspan-idkdcommandlinespankd-command-line"></a><span id="KD_Command_Line"></span><span id="kd_command_line"></span><span id="KD_COMMAND_LINE"></span>KD 命令行


通过输入运行调试器后，还可以打开转储文件[ **.opendump （打开转储文件）** ](-opendump--open-dump-file-.md)命令后, 跟[ **g （转向）** ](g--go-.md).

 

 





