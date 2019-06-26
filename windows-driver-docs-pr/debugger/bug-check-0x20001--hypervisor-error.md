---
title: Bug 检查 0x20001 HYPERVISOR_ERROR
description: HYPERVISOR_ERROR bug 检查具有 0x00020001 值。 这表示虚拟机监控程序遇到致命错误。
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
ms.openlocfilehash: 59e8dd80d5a4945e1aa86a3bf3e3f7ccd902a377
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67367543"
---
# <a name="bug-check-0x20001-hypervisorerror"></a>Bug 检查 0x20001：虚拟机监控程序\_错误


虚拟机监控程序\_错误 bug 检查的值为 0x00020001。 这表示虚拟机监控程序遇到致命错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。

## <a name="hypervisorerror-parameters"></a>虚拟机监控程序\_错误参数


| 参数 | 描述 |
|-----------|-------------|
| 1         | 保留    |
| 2         | 保留    |
| 3         | 保留    |
| 4         | 保留    |

## <a name="resolution"></a>分辨率 

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，可以非常确定根本原因。