---
title: Bug 检查 0x20001 HYPERVISOR_ERROR
description: HYPERVISOR_ERROR bug 检查的值为0x00020001。 这表示虚拟机监控程序遇到错误。
ms.assetid: 5F62DEEA-D192-46ED-827C-021A749D7091
keywords:
- Bug 检查 0x20001 HYPERVISOR_ERROR
- HYPERVISOR_ERROR
ms.date: 05/15/2020
topic_type:
- apiref
api_name:
- HYPERVISOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 067d8df4d045e11eb96de2a78d10923333f4b6b1
ms.sourcegitcommit: 4d1ed685d198629f792d287619621a87ca42c26f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435369"
---
# <a name="bug-check-0x20001-hypervisor_error"></a>Bug 检查0x20001：虚拟机监控程序 \_ 错误

虚拟机监控程序 \_ 错误检查的值为0x00020001。 这表示虚拟机监控程序遇到错误。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="hypervisor_error-parameters"></a>虚拟机监控程序 \_ 错误参数


| 参数 | 说明 |
|-----------|-------------|
| 1         | 保留    |
| 2         | 保留    |
| 3         | 保留    |
| 4         | 保留    |

## <a name="resolution"></a>解决方法

[**！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
