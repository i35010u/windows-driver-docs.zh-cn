---
title: 检查堆栈跟踪
description: 检查堆栈跟踪
keywords:
- 调试器引擎 API，堆栈跟踪
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e238b54f20ffc696ad673da7410c32eb65daf9b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829735"
---
# <a name="examining-the-stack-trace"></a>检查堆栈跟踪


*调用堆栈* 包含线程进行的函数调用的数据。 每个函数调用的数据称为一个 *堆栈帧* ，并包括返回地址、传递给函数的参数以及函数的局部变量。 每次调用函数时，新的堆栈帧就会被推送到堆栈的顶部。 当该函数返回时，堆栈帧将从堆栈中弹出。

每个线程都有自己的调用堆栈，表示在该线程中进行的调用。

若要获取堆栈跟踪，请使用 [**GetStackTrace**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace) 和 [**GetContextStackTrace**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace)方法。 可以使用 [**OutputStackTrace**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace) 和 [**OutputContextStackTrace**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)打印堆栈跟踪。

 

