---
title: 调试运行到游标
description: 调试运行到游标
keywords:
- 调试运行到游标
- 控制目标，调试 "运行到光标处"
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 26c9ec052a141600ff31faf06fa63677ea69aa66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830267"
---
# <a name="debug--run-to-cursor"></a>调试 | 运行到光标处


## <span id="ddk_debug_run_to_cursor_dbg"></span><span id="DDK_DEBUG_RUN_TO_CURSOR_DBG"></span>


单击 "**调试**" 菜单上的 "**运行到光标处**"，恢复在目标上运行的。 如果在 " [反汇编" 窗口](disassembly-window.md) 或 " [源](source-window.md) " 窗口中的指令上插入游标，然后执行此操作，则 WinDbg 会执行当前指令中的所有指令，直至所选的指令。

此命令等效于按 F7 或 CTRL + F10，或者单击 " **运行到光标处 (" ctrl + F10 或 F7)** 按钮 (![ 工具栏上的 "运行到光标处" 按钮) 屏幕截图 ](images/tbcursor.png) 。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关此操作的效果、发出此命令的其他方法以及用于控制程序执行的其他方法的详细信息，请参阅 [控制目标](controlling-the-target.md)。

 

 





