---
title: WinDbg 预览的视图菜单
description: 本部分介绍如何使用视图菜单。
ms.date: 08/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ddc15ec2dfc944a782910eecf35b28d2747cc2c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564966"
---
# <a name="windbg-preview---view-menu"></a>WinDbg 预览的视图菜单 

本部分介绍如何使用在 WinDbg 预览视图菜单。

![在调试器中的视图菜单](images/windbgx-view-menu.png)

视图菜单将打开新窗口以每个项，或将焦点移到现有窗口，如果已打开。

## <a name="command"></a>Command 
命令窗口允许您输入的调试器命令。 有关调试器命令的详细信息，请参阅[调试器命令](debugger-commands.md)。

## <a name="watch"></a>观看 

监视窗口，可监视本地变量和寄存器。 

局部变量和监视窗口基于从 dx 命令使用的数据模型。 这意味着局部变量和监视窗口将受益于任何 NatVis 或 JavaScript 扩展已加载，并支持完整的 LINQ 查询，就像 dx 命令一样。 有关数据模型的详细信息，请参阅[WinDbg 预览版-数据模型](windbg-data-model-preview.md)。

## <a name="locals"></a>局部变量
局部变量窗口显示当前作用域中的本地变量的所有信息。 局部变量窗口将重点介绍在上一次的代码执行期间更改的值。

![在调试器中的局部变量窗口](images/windbgx-locals-window.png)

## <a name="registers"></a>寄存器

寄存器可用时显示处理器寄存器的内容。 有关注册的详细信息，请参阅[注册](registers.md)并[查看和编辑注册在 WinDbg 中](registers-window.md)。

## <a name="memory"></a>内存

使用内存窗口中显示的内存位置。 除了提供内存地址，可以使用 $scopeip 和 $eventip 等伪寄存器值来检查内存。 预追加 @ 符号，以在内存窗口，例如，使用伪寄存器值`@$scopeip`。 有关详细信息，请参阅[伪寄存器语法](pseudo-register-syntax.md)


## <a name="stack"></a>堆栈 

堆栈窗口用于查看当前调用堆栈。 堆栈窗口提供了基本突出显示的当前帧。 

## <a name="disassembly"></a>反汇编

反汇编窗口突出显示了当前指令和滚动时保持该位置。 

![ 在调试器中的反汇编窗口](images/windbgx-disassembly.png)


## <a name="threads"></a>线程

线程窗口中突出显示了当前线程。 


## <a name="breakpoints"></a>断点

使用断点窗口来查看、 启用和清除断点。

![ 在调试器中的反汇编窗口](images/windbgx-breakpoints-window.png)


## <a name="logs"></a>日志

 此日志位于 WinDbg 预览内部信息。 监视长时间运行的进程以及进行故障排除调试器本身可以查看该规范。 
 
 您可以继续创建传统的调试器命令日志，使用.logopen 命令。 有关的详细信息，请参阅[的日志文件保留在 WinDbg 中](keeping-a-log-file-in-windbg.md)。

## <a name="reset-windows"></a>重置 Windows

使用此函数重置到其默认位置在调试器窗口。 


## <a name="see-also"></a>请参阅

[调试使用 WinDbg 预览](debugging-using-windbg-preview.md)

 

 





