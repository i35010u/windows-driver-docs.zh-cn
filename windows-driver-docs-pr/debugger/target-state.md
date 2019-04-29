---
title: 目标状态
description: 目标状态
ms.assetid: befd6c0b-dd16-40a1-bc6b-634b354d2a75
keywords:
- 调试器引擎 API、 目标、 状态
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1881d6ab03e7f163c1ffa7dbfe9639ff7e63b393
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380493"
---
# <a name="target-state"></a>目标状态


该方法[ **OutputCurrentState** ](https://msdn.microsoft.com/library/windows/hardware/ff553206)将打印到调试器的输出流的目标的当前状态。

返回目标的当前执行状态[ **GetExecutionStatus**](https://msdn.microsoft.com/library/windows/hardware/ff546675)。 如果目标被挂起，该方法[ **SetExecutionStatus** ](https://msdn.microsoft.com/library/windows/hardware/ff556693)可用于继续执行模式之一中的执行。

该方法[ **GetReturnOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff548237)返回当前函数返回时，将执行的指令的地址。

[**GetNearInstruction** ](https://msdn.microsoft.com/library/windows/hardware/ff547197)返回相对于给定地址的指令的位置。

### <a name="span-idexaminingthestacktracespanspan-idexaminingthestacktracespanexamining-the-stack-trace"></a><span id="examining_the_stack_trace"></span><span id="EXAMINING_THE_STACK_TRACE"></span>检查堆栈跟踪

一个*调用堆栈*包含由线程进行函数调用的数据。 每个函数调用的数据称为*堆栈帧*并包含返回的地址传递给函数，并且该函数的本地变量的参数。 每次进行函数调用时，新的堆栈帧推送到堆栈的顶部。 该函数返回时，会在堆栈中弹出堆栈帧。 每个线程都具有其自己的调用堆栈，它表示该线程中所做的调用。

**请注意**  不是所有函数调用的数据可以存储在堆栈帧。 参数和本地变量，有时，可以存储在寄存器中。

 

若要检索调用堆栈或*堆栈跟踪*，使用方法[ **GetStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff548425)并[ **GetContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff545748). 可以使用打印堆栈跟踪[ **OutputStackTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff553252)并[ **OutputContextStackTrace**](https://msdn.microsoft.com/library/windows/hardware/ff553203)。

 

 





