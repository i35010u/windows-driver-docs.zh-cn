---
title: Bug 检查 0x1D6 WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
description: WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS bug 检查具有 0x000001D6 值。 它指示工作线程更改其工作负荷类，并且未在返回之前恢复它。
keywords:
- Bug 检查 0x1D6 WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
- WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
ms.date: 01/11/2019
topic_type:
- apiref
api_name:
- WORKER_THREAD_RETURNED_WITH_NON_DEFAULT_WORKLOAD_CLASS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e7c3a0e5a80475c9213ba58f8a22fbaa6480b3cf
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239362"
---
# <a name="bug-check-0x1d6-workerthreadreturnedwithnondefaultworkloadclass"></a>Bug 检查 0x1D6：辅助角色\_线程\_返回\_WITH\_非\_默认\_工作负荷\_类

辅助角色\_线程\_返回\_WITH\_非\_默认\_工作负荷\_类 bug 检查的值为 0x000001D6。 它指示工作线程更改其工作负荷类，并且未在返回之前恢复它。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="workerthreadreturnedwithnondefaultworkloadclass-parameters"></a>辅助角色\_线程\_返回\_WITH\_非\_默认\_工作负荷\_类参数

|参数|描述|
|-------- |---------- |
|1| 辅助角色 (在此查找负责驱动程序使用 ln) 例程的地址 |
|2| 当前工作负荷类值。 |
|3| 工作项的参数。 |
|4| 工作项的地址。 |

## <a name="cause"></a>原因
-----

工作线程更改其工作负荷类和未返回之前恢复它。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

