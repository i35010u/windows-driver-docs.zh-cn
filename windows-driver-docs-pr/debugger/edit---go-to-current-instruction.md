---
title: 编辑中转到当前指令
description: 编辑中转到当前指令
keywords:
- 编辑中转到当前指令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc5c50a4404ba23df548e1e34f2f99856aabf9f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828891"
---
# <a name="edit--go-to-current-instruction"></a>编辑 | 转到当前指令


## <span id="ddk_edit_go_to_current_instruction_dbg"></span><span id="DDK_EDIT_GO_TO_CURRENT_INSTRUCTION_DBG"></span>


在 "**编辑**" 菜单上单击 "**前往当前说明**"，打开包含当前指令的 "调试信息" 窗口并突出显示此指令。

此命令等效于使用数字键盘上的星号键 (按 ALT + 星号) 。

如果当前指令对应于已知的源文件，则 WinDbg 会打开包含此源文件的 [源窗口](source-window.md) 。 如果不存在这样的窗口，则 WinDbg 将打开一个窗口。 将突出显示当前行。

如果当前指令不在已知的源文件中并且 "反汇编" [窗口](disassembly-window.md) 处于打开状态，则 WinDbg 会打开 "反汇编" 窗口并突出显示当前行。 但是，如果关闭 "反汇编" 窗口，则 " **转向当前指令** " 命令将不会打开它。

此命令只更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

 

 





