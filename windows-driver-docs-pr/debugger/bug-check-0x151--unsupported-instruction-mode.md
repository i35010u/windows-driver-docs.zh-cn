---
title: Bug 检查 0x151 UNSUPPORTED_INSTRUCTION_MODE
description: UNSUPPORTED_INSTRUCTION_MODE bug 检查具有 0x00000151 值。
ms.assetid: 2FB679D8-9FA3-423D-BCA1-5EDE88C78FBF
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
ms.openlocfilehash: 59d5b1085cdf9867b2e780cdfc1a1b7d60feb884
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362195"
---
# <a name="bug-check-0x151-unsupportedinstructionmode"></a>Bug 检查 0x151：不支持\_指令\_模式


不支持\_指令\_模式 bug 检查的值为 0x00000151。 这表示尝试使用不受支持的处理器指令模式下 （例如，正在执行经典 ARM 指令而不是 ThumbV2 指令） 执行代码。 这不是允许。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


## <a name="unsupportedinstructionmode-parameters"></a>不支持\_指令\_模式参数


| 参数 | 描述                                    |
|-----------|------------------------------------------------|
| 1         | 当检测到问题时的程序计数器。 |
| 2         | 陷阱帧                                     |
| 3         | 保留                                       |
| 4         | 保留                                       |

 

 

 




