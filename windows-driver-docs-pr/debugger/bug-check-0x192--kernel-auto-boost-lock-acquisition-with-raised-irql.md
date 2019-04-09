---
title: Bug Check 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
description: KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL bug 检查指示执行在 DISPATCH_LEVEL 或更高版本时已获取跟踪的 AutoBoost 锁。
ms.assetid: D88EF2CC-26DC-44D8-80CB-18D058C6A413
keywords:
- Bug Check 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85e492a9344cc7427d9eba3ee2b459b80807a2ce
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238748"
---
# <a name="bug-check-0x192-kernelautoboostlockacquisitionwithraisedirql"></a>Bug 检查 0x192：内核\_自动\_BOOST\_锁\_采集\_WITH\_凸起\_IRQL


内核\_自动\_BOOST\_锁\_采集\_WITH\_凸起\_IRQL bug 检查的值为 0x00000192。 这指示执行在调度时已获取跟踪的 AutoBoost 锁\_级别或更高版本。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="kernelautoboostlockacquisitionwithraisedirql-parameters"></a>内核\_自动\_BOOST\_锁\_采集\_WITH\_凸起\_IRQL 参数


| 参数 | 描述                             |
|-----------|-----------------------------------------|
| 1         | 该线程的地址               |
| 2         | 锁地址                        |
| 3         | 获取锁所在的 IRQL |
| 4         | 保留                                |

 

<a name="cause"></a>原因
-----

调用方不能阻止 APC 上面锁\_级别，因为可能以独占方式中断线程，这会导致死锁持有锁。

 

 




