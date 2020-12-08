---
title: 堆栈展开信息不可用
description: 堆栈展开信息不可用
keywords:
- '堆栈展开信息不可用 (警告) '
- '调用堆栈，堆栈展开信息不可用 (警告) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d5c2be211597887db94b6f19a70f3c95991c5fcc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836857"
---
# <a name="stack-unwind-information-not-available"></a>堆栈展开信息不可用


## <span id="ddk_stack_unwind_information_not_available_dbg"></span><span id="DDK_STACK_UNWIND_INFORMATION_NOT_AVAILABLE_DBG"></span>


调试器检查调用堆栈时，可能会显示消息 "堆栈展开信息不可用。 以下框架可能是错误的。 "

此警告表明，此消息正确后，调试器不一定会列出调用堆栈中列出的帧。

为了跟踪调用堆栈，调试器会检查堆栈并分析已使用堆栈的函数。 这使它能够标识形成调用堆栈的返回地址链。 但是，此过程需要包含使用堆栈的函数的每个模块的符号信息。

如果此符号信息不可用，则会强制调试器最大程度地推测返回地址的帧。 此时会显示此警告信息，指示在此点之后调用堆栈的不确定性质。

 

 





