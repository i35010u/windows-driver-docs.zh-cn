---
title: 目标状态
description: 目标状态
ms.assetid: befd6c0b-dd16-40a1-bc6b-634b354d2a75
keywords:
- 调试器引擎 API，目标，状态
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6a80216ad6961bb5f3df2773634a1e5775de532e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834271"
---
# <a name="target-state"></a>目标状态


方法[**OutputCurrentState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputcurrentstate)将目标的当前状态打印到调试器的输出流。

[**GetExecutionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getexecutionstatus)返回目标的当前执行状态。 如果已挂起目标，则可以使用方法[**SetExecutionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setexecutionstatus) ，在执行模式之一中继续执行。

方法[**GetReturnOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getreturnoffset)返回在当前函数返回时要执行的指令的地址。

[**GetNearInstruction**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getnearinstruction)返回相对于给定地址的指令的位置。

### <a name="span-idexamining_the_stack_tracespanspan-idexamining_the_stack_tracespanexamining-the-stack-trace"></a><span id="examining_the_stack_trace"></span><span id="EXAMINING_THE_STACK_TRACE"></span>检查堆栈跟踪

*调用堆栈*包含线程进行的函数调用的数据。 每个函数调用的数据称为一个*堆栈帧*，并包括返回地址、传递给函数的参数以及函数的局部变量。 每次调用函数时，新的堆栈帧将被推送到堆栈的顶部。 当该函数返回时，堆栈帧将从堆栈中弹出。 每个线程都有自己的调用堆栈，该堆栈表示在该线程中进行的调用。

**请注意**   不能将函数调用的所有数据都存储在堆栈帧中。 有时，参数和局部变量可以存储在寄存器中。

 

若要检索调用堆栈或*堆栈跟踪*，请使用[**GetStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace)和[**GetContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace)方法。 可以使用[**OutputStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace)和[**OutputContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)打印堆栈跟踪。

 

 





