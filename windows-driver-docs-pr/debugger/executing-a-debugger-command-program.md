---
title: 执行调试器命令程序
description: 执行调试器命令程序
ms.assetid: ad28a5d6-0d6a-42c0-82f3-6760a8c773ab
keywords:
- 调试器命令程序中执行
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 412bb20e950615b2247f31a52ba16ba2ea990b2d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525284"
---
# <a name="executing-a-debugger-command-program"></a>执行调试器命令程序


## <span id="ddk_debugger_command_program_execution_dbg"></span><span id="DDK_DEBUGGER_COMMAND_PROGRAM_EXECUTION_DBG"></span>


可以通过以下方式之一执行调试器命令程序：

-   输入中的语句的所有[调试器命令窗口](debugger-command-window.md)作为单个字符串，与单个语句和命令之间用分号分隔。

-   在带有单个语句和命令之间用分号分隔的单个行上的脚本文件中添加的所有语句。 然后，使用中所述的方法之一运行此脚本文件[使用脚本文件](using-script-files.md)。

-   在包含单独的行上每个语句的脚本文件中添加的所有语句。 （或者，将分语句由回车符和分号的任意组合。）然后，使用运行此脚本文件[  **$ &gt; &lt; （运行脚本文件）** ](-----------------------a---run-script-file-.md)或 **$$ &gt; &lt; （运行脚本文件）** 命令。 这些命令打开指定的脚本文件，用分号，替换所有回车符并执行单个命令块为生成的文本。

 

 





