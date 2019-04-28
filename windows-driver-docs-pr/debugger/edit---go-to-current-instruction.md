---
title: 编辑转到当前指令
description: 编辑转到当前指令
ms.assetid: 7bc57ac1-1de6-4534-836b-132e3b072ae5
keywords:
- 编辑转到当前指令
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b81ca7013fb3506972a1fd8956dd0fc4badcb49
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331400"
---
# <a name="edit--go-to-current-instruction"></a>编辑 | 转到当前指令


## <span id="ddk_edit_go_to_current_instruction_dbg"></span><span id="DDK_EDIT_GO_TO_CURRENT_INSTRUCTION_DBG"></span>


单击**转到当前指令**上**编辑**菜单可打开包含当前指令的调试信息窗口，从而突出显示此指令。

此命令相当于按下 ALT + 星号 （使用数字键盘上的星号键）。

如果当前指令对应于一个已知的源代码文件，将打开 WinDbg[源窗口](source-window.md)，其中包含此源文件。 如果不存在任何此类窗口，WinDbg 将打开一个。 突出显示当前行。

如果当前指令不是已知的源代码文件中的和[反汇编窗口](disassembly-window.md)是打开，请突出显示反汇编窗口和当前行的 WinDbg 随即打开。 但是，如果反汇编窗口已关闭，则**转到当前指令**命令不会打开。

此命令仅更改 WinDbg 显示。 此命令不会影响目标或任何其他调试器操作的执行。

 

 





