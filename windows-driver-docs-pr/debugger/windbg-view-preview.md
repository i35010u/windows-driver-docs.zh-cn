---
title: WinDbg 预览-"查看" 菜单
description: 本部分介绍如何使用 "视图" 菜单。
ms.date: 08/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2776a3e696e92261f89235390d8b8b48a2dfc9a
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209600"
---
# <a name="windbg-preview---view-menu"></a>WinDbg 预览-"查看" 菜单

本部分介绍如何使用 WinDbg Preview 中的 "视图" 菜单。

![调试器中的 "视图" 菜单](images/windbgx-view-menu.png)

"视图" 菜单将为每个项打开一个新窗口，或者将焦点移到现有窗口（如果已打开）。

## <a name="command"></a>命令 
命令窗口允许你输入调试器命令。 有关调试器命令的详细信息，请参阅[调试器命令](debugger-commands.md)。

## <a name="watch"></a>观看 

在 "监视" 窗口中，可以监视本地变量和注册。 

"局部变量" 和 "监视" 窗口均基于 dx 命令使用的数据模型。 这意味着，"局部变量" 和 "监视" 窗口将受益于已加载的任何 NatVis 或 JavaScript 扩展，并支持完整的 LINQ 查询，就像 dx 命令一样。 有关数据模型的详细信息，请参阅[WinDbg 预览-数据模型](windbg-data-model-preview.md)。

## <a name="locals"></a>&
"局部变量" 窗口显示有关当前范围内的所有本地变量的信息。 "局部变量" 窗口将突出显示在前面的代码执行过程中更改的值。

![调试器中的 "局部变量" 窗口](images/windbgx-locals-window.png)

## <a name="registers"></a>寄存器

收银机显示处理器的内容（如果可用）。 有关寄存器的详细信息，请[](registers.md)参阅[在 WinDbg 中注册和查看和编辑寄存器](registers-window.md)。

## <a name="memory"></a>内存

使用 "内存" 窗口显示内存位置。 除了提供内存地址外，还可以使用伪寄存器值（如 $scopeip 和 $eventip）来检查内存。 预先追加 @ 符号以使用 "内存" 窗口中的伪寄存器值，例如 `@$scopeip`。 有关详细信息，请参阅[伪寄存器语法](pseudo-register-syntax.md)


## <a name="stack"></a>重叠 

使用 "堆栈" 窗口查看当前调用堆栈。 "堆栈" 窗口提供当前帧的基本突出显示。 

## <a name="disassembly"></a>反汇编

"反汇编" 窗口将突出显示当前指令并在滚动时保留该位置。 

![ 调试器中的 "反汇编" 窗口](images/windbgx-disassembly.png)


## <a name="threads"></a>线程

"线程" 窗口将突出显示当前线程。 


## <a name="breakpoints"></a>断点

使用 "断点" 窗口可以查看、启用和清除断点。

![ 调试器中的 "反汇编" 窗口](images/windbgx-breakpoints-window.png)


## <a name="logs"></a>日志

 此日志为 WinDbg 预览版。 可以查看它来监视长时间运行的进程，并对调试器本身进行故障排除。 
 
 可以使用 logopen 命令继续创建传统的调试器命令日志。 有关此方面的详细信息，请参阅[在 WinDbg 中保留日志文件](keeping-a-log-file-in-windbg.md)。

## <a name="reset-windows"></a>重置窗口

使用此函数可将调试器窗口重置为其默认位置。 


## <a name="see-also"></a>另请参阅

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)

 

 





