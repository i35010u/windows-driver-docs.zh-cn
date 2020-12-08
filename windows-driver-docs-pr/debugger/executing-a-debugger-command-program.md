---
title: 执行调试器命令程序
description: 执行调试器命令程序
keywords:
- 调试器命令程序，执行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 348c49a4677328338f034d137e643105a75cff89
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838221"
---
# <a name="executing-a-debugger-command-program"></a>执行调试器命令程序


## <span id="ddk_debugger_command_program_execution_dbg"></span><span id="DDK_DEBUGGER_COMMAND_PROGRAM_EXECUTION_DBG"></span>


可以通过以下方式之一执行调试器命令程序：

-   以单个字符串的形式输入调试器中的所有语句 [命令窗口](debugger-command-window.md) ，其中各个语句和命令用分号分隔。

-   将脚本文件中的所有语句添加到单个行上，单独的语句和命令用分号分隔。 然后，使用 " [脚本文件](using-script-files.md)" 中所述的方法之一运行此脚本文件。

-   将所有语句添加到脚本文件中，并将每个语句置于单独的行中。  (或者，用回车符和分号的任意组合分隔语句。 ) 然后，请使用 [**$ &gt; &lt; (运行脚本文件)**](-----------------------a---run-script-file-.md)或 **$$ &gt; &lt; (运行脚本文件)** 命令运行此脚本文件。 这些命令将打开指定的脚本文件，将所有回车返回替换为分号，并将生成的文本作为单个命令块执行。

 

 





