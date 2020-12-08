---
title: Bug 检查 0x131 INVALID_EXTENDED_PROCESSOR_STATE
description: INVALID_EXTENDED_PROCESSOR_STATE bug 检查的值为0x00000131。 这表示在保存或还原扩展处理器状态时检测到无效的参数组合。
keywords:
- Bug 检查 0x131 INVALID_EXTENDED_PROCESSOR_STATE
- INVALID_EXTENDED_PROCESSOR_STATE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_EXTENDED_PROCESSOR_STATE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d5bbd028ec83415b3de959297cd1522c84cde38a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815235"
---
# <a name="bug-check-0x131-invalid_extended_processor_state"></a>Bug 检查0x131： \_ 扩展 \_ 处理器 \_ 状态无效


无效的 \_ 扩展 \_ 处理器 \_ 状态 bug 检查的值为0x00000131。 这表示在保存或还原扩展处理器状态时检测到无效的参数组合。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_extended_processor_state-parameters"></a>\_扩展 \_ 处理器 \_ 状态参数无效


参数1指示验证失败的有效性。

| 参数 | 描述                                                                     |
|-----------|---------------------------------------------------------------------------------|
| 1         | 0-传递的功能掩码无效或未启用扩展处理器状态。 |
| 2         | 如果启用扩展状态，则为非零值。                                           |
| 3         | 功能掩码的低32位。                                            |
| 4         | 功能掩码的高32位。                                           |

 

| 参数 | 描述                                                                                    |
|-----------|------------------------------------------------------------------------------------------------|
| 1         | 1-尝试保存或还原扩展状态的操作在 IRQL 高于调度级别时进行 \_ 。 |
| 2         | IRQL                                                                                       |
| 3         | 预留                                                                                       |
| 4         | 预留                                                                                       |

 

| 参数 | 描述                                                     |
|-----------|-----------------------------------------------------------------|
| 1         | 2-以前保存的状态用于相等或更高的级别。 |
| 2         | 保存的级别。                                                |
| 3         | 当前级别。                                              |
| 4         | 预留                                                        |

 

| 参数 | 描述                                               |
|-----------|-----------------------------------------------------------|
| 1         | 3-以前保存的状态适用于不同的线程。 |
| 2         | 已保存的线程。                                         |
| 3         | 当前线程。                                       |
| 4         | 预留                                                  |

 

| 参数 | 描述                                          |
|-----------|------------------------------------------------------|
| 1         | 4-以前保存的状态适用于不同的级别。 |
| 2         | 保存的级别。                                     |
| 3         | 当前级别。                                   |
| 4         | 预留                                             |

 

 

 




