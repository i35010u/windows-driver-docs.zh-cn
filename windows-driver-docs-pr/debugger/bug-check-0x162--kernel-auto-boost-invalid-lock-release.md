---
title: Bug 检查 0x162 KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
description: KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE bug 检查的值为0x00000162。 这表示由 AutoBoost 跟踪的锁由不拥有该锁的线程释放。
keywords:
- Bug 检查 0x162 KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
- KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 10b6bd6cf49e5343653077ca8090be41ad60cf1d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830763"
---
# <a name="bug-check-0x162-kernel_auto_boost_invalid_lock_release"></a>Bug 检查0x162：内核 \_ 自动 \_ 提升 \_ 无效 \_ 锁定 \_ 版本


内核 \_ 自动 \_ 提升 \_ 无效 \_ 锁定 \_ 发布 bug 检查的值为0x00000162。 这表示由 AutoBoost 跟踪的锁由不拥有该锁的线程释放。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="kernel_auto_boost_invalid_lock_release-parameters"></a>内核 \_ 自动 \_ 提升 \_ 无效的 \_ 锁定 \_ 释放参数


| 参数 | 描述                  |
|-----------|------------------------------|
| 1         | 线程的地址    |
| 2         | 锁定地址             |
| 3         | 线程的会话 ID |
| 4         | 预留                     |

 

<a name="cause"></a>原因
-----

当某个线程代表另一个线程释放锁定时，通常会发生这种情况， (该线程对于启用了 AutoBoost 跟踪的) 是合法的，或者当某个线程尝试释放不再拥有的锁时。

 

 




