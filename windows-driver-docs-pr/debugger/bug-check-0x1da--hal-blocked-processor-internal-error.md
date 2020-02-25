---
title: Bug 检查 1DA HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
description: HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR 的值为0x000001DA。
keywords:
- Bug 检查 0x1DA HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
- HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
ms.date: 02/20/2020
topic_type:
- apiref
api_name:
- HAL_BLOCKED_PROCESSOR_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a251cb9ce152aaf974d231fe519db718e20b55e9
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77530335"
---
# <a name="bug-check-0x1da-hal_blocked_processor_internal_error"></a>Bug 检查0x1DA： HAL\_阻止\_处理器\_内部\_错误

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

HAL\_阻止\_PROCESSOR\_内部\_错误的值为0x000001DA。 它表示在已阻止的处理器库中检测到内部错误。

## <a name="hal_blocked_processor_internal_error-parameters"></a>HAL\_阻止\_处理器\_内部\_错误参数

以下参数显示在蓝色屏幕上。

| 参数 |                        说明              |
|-----------|-------------------------------------------------|
|     1     | 失败类型-请参阅下面                     |
|     2     | 请见下文。                                      |
|     3     | 请见下文。                                      |
|     4     | 请见下文。                                      |

## <a name="parameter-one-values"></a>参数一个值

```plaintext
            0x01 : Library initialization failure
                2 - NT status code
            0x02 : Processor start failure
                2 - Processor index
                3 - APIC ID
            0x03 : PPM package ID query failure
                2 - Processor index
            0x04 : PPM operation failure
                2 - Operation
                    0x01 : MSR read
                    0x02 : MSR write
                    0x03 : I/O port read
                    0x04 : I/O port write
                    0x05 : Idle state registration
                3 - Processor index
                4 - PPM mailbox
            0x05 : A blocked processor has encountered a fatal exception.
                2 - Processor index
                3 - Vector number
                4 - Trap frame
            0x06 : PPM operation timeout
                2 - Operation
                    0x01 : MSR read
                    0x02 : MSR write
                    0x03 : I/O port read
                    0x04 : I/O port write
                    0x05 : Idle state registration
                3 - Processor index
                4 - PPM mailbox
```
