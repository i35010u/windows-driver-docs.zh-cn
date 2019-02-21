---
title: 堆栈展开信息不可用
description: 堆栈展开信息不可用
ms.assetid: 82260f85-780b-4f30-bebd-62faed6efeeb
keywords:
- 堆栈展开信息不可用 （警告）
- 调用堆栈，堆栈展开信息不可用 （警告）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16a3eafedf8830351550145b6724a2fbf509647f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540955"
---
# <a name="stack-unwind-information-not-available"></a>堆栈展开信息不可用


## <span id="ddk_stack_unwind_information_not_available_dbg"></span><span id="DDK_STACK_UNWIND_INFORMATION_NOT_AVAILABLE_DBG"></span>


当调试器检查调用堆栈时，它可能会显示消息"堆栈展开信息不可用。 以下帧可能有误。"

此警告表明，调试器不是特定帧调用堆栈中的列出后此消息正确。

若要跟踪的调用堆栈，调试器会检查堆栈和分析堆栈使用过的函数。 这允许它确定窗体调用堆栈的返回地址的链。 但是，此过程需要包含使用堆栈的函数的每个模块的符号信息。

如果此符号信息不可用，强制调试器进行最佳猜测的帧是返回地址。 显示此警告信息以指示此点后的调用堆栈不确定的性质。

 

 





