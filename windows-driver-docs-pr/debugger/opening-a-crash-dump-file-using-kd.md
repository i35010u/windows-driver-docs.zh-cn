---
title: 使用 KD 打开转储文件
description: 使用 KD 打开转储文件
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f216c4519c56eafda3c3c0757320bed3b17aceb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833619"
---
# <a name="opening-a-dump-file-using-kd"></a>使用 KD 打开转储文件


## <a name="span-idcommand_promptspanspan-idcommand_promptspanspan-idcommand_promptspancommand-prompt"></a><span id="Command_Prompt"></span><span id="command_prompt"></span><span id="COMMAND_PROMPT"></span>命令提示符


在命令提示符窗口中，您可以在启动 KD 时打开转储文件。 使用以下命令。

**kd-y** *SymbolPath* **-i** *ImagePath* **-z** *DumpFileName*

**-V** 选项 (详细模式) 也很有用。 有关命令行语法的详细信息，请参阅 [**KD Command-Line Options**](kd-command-line-options.md)。

## <a name="span-idkd_command_linespanspan-idkd_command_linespanspan-idkd_command_linespankd-command-line"></a><span id="KD_Command_Line"></span><span id="kd_command_line"></span><span id="KD_COMMAND_LINE"></span>KD 命令行


您还可以通过输入 [**opendump (打开转储文件)**](-opendump--open-dump-file-.md) 命令，然后按 [**g (中转)**](g--go-.md)，在调试器运行后打开转储文件。

 

 





