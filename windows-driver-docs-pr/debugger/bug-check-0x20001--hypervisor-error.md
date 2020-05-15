---
title: Bug 检查 0x20001 HYPERVISOR_ERROR
description: HYPERVISOR_ERROR bug 检查的值为0x00020001。 这表示虚拟机监控程序遇到错误。
ms.assetid: 5F62DEEA-D192-46ED-827C-021A749D7091
keywords:
- Bug 检查 0x20001 HYPERVISOR_ERROR
- HYPERVISOR_ERROR
ms.date: 04/12/2019
topic_type:
- apiref
api_name:
- HYPERVISOR_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b3822317651aa3d6a1b0293f2561e70d371551f9
ms.sourcegitcommit: b35469bbcabee996af70bcbd8564184f547a8c57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/15/2020
ms.locfileid: "83406247"
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

[**！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用。
