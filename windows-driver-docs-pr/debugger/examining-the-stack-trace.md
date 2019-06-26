---
title: 检查堆栈跟踪
description: 检查堆栈跟踪
ms.assetid: ca203f29-841f-411e-915a-81abaa96a8e6
keywords:
- 调试器引擎 API，堆栈跟踪
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef7763af3d112110a3ab0e06c1c97b02282fcfe1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361371"
---
# <a name="examining-the-stack-trace"></a>检查堆栈跟踪


一个*调用堆栈*包含由线程进行的函数调用的数据。 每个函数调用的数据称为*堆栈帧*并包含返回的地址传递给函数，并且该函数的本地变量的参数。 每次函数调用进行新的堆栈帧时推送到堆栈的顶部。 该函数返回时，会在堆栈中弹出堆栈帧。

每个线程都具有其自己的调用堆栈，表示该线程中进行的调用。

若要获取堆栈跟踪，请使用方法[ **GetStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-getstacktrace)并[ **GetContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-getcontextstacktrace)。 可以使用打印堆栈跟踪[ **OutputStackTrace** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-outputstacktrace)并[ **OutputContextStackTrace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol4-outputcontextstacktrace)。

 

 





