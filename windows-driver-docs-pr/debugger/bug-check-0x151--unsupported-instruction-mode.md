---
title: Bug 检查 0x151 UNSUPPORTED_INSTRUCTION_MODE
description: UNSUPPORTED_INSTRUCTION_MODE bug 检查的值为0x00000151。
keywords:
- Bug 检查 0x151 UNSUPPORTED_INSTRUCTION_MODE
- UNSUPPORTED_INSTRUCTION_MODE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- UNSUPPORTED_INSTRUCTION_MODE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 302a55fd4de0e5c04916475f70b043eef7728beb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790687"
---
# <a name="bug-check-0x151-unsupported_instruction_mode"></a>Bug 检查0x151：不支持的 \_ 指令 \_ 模式


不受支持的 \_ 指令 \_ 模式 bug 检查的值为0x00000151。 这表明尝试使用不受支持的处理器指令模式执行代码 (例如，执行经典 ARM 指令而不是 ThumbV2 指令) 。 这是不允许的。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="unsupported_instruction_mode-parameters"></a>不支持的 \_ 指令 \_ 模式参数


| 参数 | 描述                                    |
|-----------|------------------------------------------------|
| 1         | 检测到问题时的程序计数器。 |
| 2         | 捕获帧                                     |
| 3         | 预留                                       |
| 4         | 预留                                       |

 

 

 




