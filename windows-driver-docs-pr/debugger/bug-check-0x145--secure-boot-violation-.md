---
title: Bug 检查 0x145 SECURE_BOOT_VIOLATION
description: SECURE_BOOT_VIOLATION bug 检查具有 0x00000145 值。 这表示无法启动安全启动策略实施。
ms.assetid: C877C655-D94D-45B5-82DB-1361F0B020D2
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
ms.openlocfilehash: bf036f42c57d31dbe389a5023f7c280b0ceff51a
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520124"
---
# <a name="bug-check-0x145-securebootviolation"></a>Bug 检查 0x145：安全\_启动\_冲突


SECURE\_启动\_冲突错误检查的值为 0x00000145。 这表示无法由于无效的策略或所需的操作未完成启动安全启动策略实施。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="securebootviolation-parameters"></a>安全\_启动\_冲突参数


| 参数 | 描述                        |
|-----------|------------------------------------|
| 1         | 失败的状态代码。    |
| 2         | 安全启动策略的地址。 |
| 3         | 安全启动策略的大小。    |
| 4         | 保留                           |

 

 

 




