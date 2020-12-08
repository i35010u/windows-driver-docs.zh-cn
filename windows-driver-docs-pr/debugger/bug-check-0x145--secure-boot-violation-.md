---
title: Bug 检查 0x145 SECURE_BOOT_VIOLATION
description: SECURE_BOOT_VIOLATION bug 检查的值为0x00000145。 这表明无法启动安全启动策略强制。
keywords:
- Bug 检查 0x145 SECURE_BOOT_VIOLATION
- SECURE_BOOT_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SECURE_BOOT_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 53c6abf2722df5c88e1bb212f756571e7c313e19
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794031"
---
# <a name="bug-check-0x145-secure_boot_violation"></a>Bug 检查0x145：安全 \_ 启动 \_ 冲突


安全 \_ 启动 \_ 冲突 bug 检查的值为0x00000145。 这表示由于策略无效或未完成所需的操作，无法启动安全启动策略强制。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="secure_boot_violation-parameters"></a>安全 \_ 启动 \_ 冲突参数


| 参数 | 描述                        |
|-----------|------------------------------------|
| 1         | 故障的状态代码。    |
| 2         | 安全启动策略的地址。 |
| 3         | 安全启动策略的大小。    |
| 4         | 预留                           |

 

 

 




