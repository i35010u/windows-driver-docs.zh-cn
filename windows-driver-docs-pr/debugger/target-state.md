---
title: 目标状态
description: 目标状态
ms.assetid: befd6c0b-dd16-40a1-bc6b-634b354d2a75
keywords:
- 调试器引擎 API、 目标、 状态
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 058e1649f6741d354797932948592c9bd621bde1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368650"
---
# <a name="target-state"></a>目标状态


该方法[ **OutputCurrentState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputcurrentstate)将打印到调试器的输出流的目标的当前状态。

返回目标的当前执行状态[ **GetExecutionStatus**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getexecutionstatus)。 如果目标被挂起，该方法[ **SetExecutionStatus** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-setexecutionstatus)可用于继续执行模式之一中的执行。

该方法[ **GetReturnOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getreturnoffset)返回当前函数返回时，将执行的指令的地址。

[**GetNearInstruction** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getnearinstruction)返回相对于给定地址的指令的位置。

### <a name="span-idexaminingthestacktracespanspan-idexaminingthestacktracespanexamining-the-stack-trace"></a><span id="examining_the_stack_trace"></span><span id="EXAMINING_THE_STACK_TRACE"></span>检查堆栈跟踪

一个*调用堆栈*包含由线程进行函数调用的数据。 每个函数调用的数据称为*堆栈帧*并包含返回的地址传递给函数，并且该函数的本地变量的参数。 每次进行函数调用时，新的堆栈帧推送到堆栈的顶部。 该函数返回时，会在堆栈中弹出堆栈帧。 每个线程都具有其自己的调用堆栈，它表示该线程中所做的调用。

**请注意**  不是所有函数调用的数据可以存储在堆栈帧。 参数和本地变量，有时，可以存储在寄存器中。

 

若要检索调用堆栈或*堆栈跟踪*，使用方法[ **GetStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace)并[ **GetContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace). 可以使用打印堆栈跟踪[ **OutputStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace)并[ **OutputContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)。

 

 





