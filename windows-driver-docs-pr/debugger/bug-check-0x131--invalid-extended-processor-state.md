---
title: Bug 检查 0x131 INVALID_EXTENDED_PROCESSOR_STATE
description: INVALID_EXTENDED_PROCESSOR_STATE bug 检查具有 0x00000131 值。 这表示保存或还原扩展的处理器状态时检测到无效的参数组合。
ms.assetid: 72EEA46A-1E96-4B07-A7E6-40DAE4641B20
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
ms.openlocfilehash: e84f2ba30c56734a6a10743206ae52b2af469296
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351237"
---
# <a name="bug-check-0x131-invalidextendedprocessorstate"></a>Bug 检查 0x131：无效\_扩展\_处理器\_状态


无效\_扩展\_处理器\_状态 bug 检查的值为 0x00000131。 这表示保存或还原扩展的处理器状态时检测到无效的参数组合。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="invalidextendedprocessorstate-parameters"></a>无效\_扩展\_处理器\_状态参数


一个指示哪个有效性检查的参数失败。

| 参数 | 描述                                                                     |
|-----------|---------------------------------------------------------------------------------|
| 1         | 0-传递无效的功能掩码或未启用扩展的处理器状态。 |
| 2         | 如果启用扩展的状态，非零值。                                           |
| 3         | 功能掩码的低 32 位。                                            |
| 4         | 功能掩码的高 32 位。                                           |

 

| 参数 | 描述                                                                                    |
|-----------|------------------------------------------------------------------------------------------------|
| 1         | 1-若要保存或恢复扩展的状态尝试在 IRQL 高于调度\_级别。 |
| 2         | IRQL                                                                                       |
| 3         | 保留                                                                                       |
| 4         | 保留                                                                                       |

 

| 参数 | 描述                                                     |
|-----------|-----------------------------------------------------------------|
| 1         | 2-以前保存的状态为相等或更高级别。 |
| 2         | 已保存的级别。                                                |
| 3         | 当前级别。                                              |
| 4         | 保留                                                        |

 

| 参数 | 描述                                               |
|-----------|-----------------------------------------------------------|
| 1         | 3-以前保存的状态是不同的线程。 |
| 2         | 已保存的线程。                                         |
| 3         | 当前线程。                                       |
| 4         | 保留                                                  |

 

| 参数 | 描述                                          |
|-----------|------------------------------------------------------|
| 1         | 4-以前保存的状态为一个不同的级别。 |
| 2         | 已保存的级别。                                     |
| 3         | 当前级别。                                   |
| 4         | 保留                                             |

 

 

 




