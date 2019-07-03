---
title: Bug Check 0x162 KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
description: KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE bug 检查具有 0x00000162 值。 这指示跟踪的 AutoBoost 的锁已释放未拥有的锁的线程。
ms.assetid: 8430B461-892C-4517-B5E1-94DCDB413B21
keywords:
- Bug Check 0x162 KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
- KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_AUTO_BOOST_INVALID_LOCK_RELEASE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 023b2f92ec406e0a6e13dbe16e105b3817890c02
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519988"
---
# <a name="bug-check-0x162-kernelautoboostinvalidlockrelease"></a>Bug 检查 0x162：内核\_自动\_BOOST\_无效\_锁\_版本


内核\_自动\_BOOST\_无效\_锁\_发布 bug 检查的值为 0x00000162。 这指示跟踪的 AutoBoost 的锁已释放未拥有的锁的线程。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="kernelautoboostinvalidlockrelease-parameters"></a>内核\_自动\_BOOST\_无效\_锁\_发布参数


| 参数 | 描述                  |
|-----------|------------------------------|
| 1         | 该线程的地址    |
| 2         | 锁地址             |
| 3         | 线程的会话 ID |
| 4         | 保留                     |

 

<a name="cause"></a>原因
-----

这通常被由于某些线程释放锁代表另一个线程 （这是不合法 AutoBoost 启用了跟踪） 时或当某个线程尝试释放不再拥有的锁时。

 

 




