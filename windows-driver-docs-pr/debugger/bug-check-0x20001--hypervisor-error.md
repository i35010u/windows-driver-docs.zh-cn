---
title: Bug 检查 0x20001 HYPERVISOR_ERROR
description: HYPERVISOR_ERROR bug 检查的值为0x00020001。 这表示虚拟机监控程序遇到错误。
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
ms.openlocfilehash: 2e61f167501e446c8c1d2a3c538ef44edf84f445
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839815"
---
# <a name="bug-check-0x20001-hypervisor_error"></a>Bug 检查0x20001：虚拟机监控程序 \_ 错误

虚拟机监控程序 \_ 错误检查的值为0x00020001。 这表示虚拟机监控程序遇到错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="hypervisor_error-parameters"></a>虚拟机监控程序 \_ 错误参数


| 参数 | 描述 |
|-----------|-------------|
| 1         | 保留    |
| 2         | 预留    |
| 3         | 预留    |
| 4         | 预留    |

## <a name="resolution"></a>解决方法

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
