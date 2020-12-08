---
title: Bug 检查 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
description: KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL bug 检查指示在 DISPATCH_LEVEL 或更高版本中执行时获取了 AutoBoost 跟踪的锁。
keywords:
- Bug 检查 0x192 KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_AUTO_BOOST_LOCK_ACQUISITION_WITH_RAISED_IRQL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bd33b6067526f8944e0148e3f78edaaccbd6cc83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814005"
---
# <a name="bug-check-0x192-kernel_auto_boost_lock_acquisition_with_raised_irql"></a>Bug 检查0x192：内核 \_ 自动 \_ 提升 \_ 锁 \_ 获取 \_ 时 \_ 引发的 \_ IRQL


\_ \_ \_ \_ \_ 使用引发的 IRQL bug 检查进行内核自动提升锁获取的 \_ \_ 值为0x00000192。 这表示在调度 \_ 级别或更高级别执行时获取了由 AutoBoost 跟踪的锁。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="kernel_auto_boost_lock_acquisition_with_raised_irql-parameters"></a>内核 \_ 自动 \_ 提升 \_ 锁 \_ 获取 \_ ，并 \_ 引发 \_ IRQL 参数


| 参数 | 描述                             |
|-----------|-----------------------------------------|
| 1         | 线程的地址               |
| 2         | 锁定地址                        |
| 3         | 在其上获取锁的 IRQL |
| 4         | 预留                                |

 

<a name="cause"></a>原因
-----

调用方不能阻塞在 APC 级别以上的锁上 \_ ，因为该锁可能被中断的线程独占处理，从而导致死锁。

 

 




