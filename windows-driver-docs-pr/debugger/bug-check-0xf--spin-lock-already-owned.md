---
title: Bug 检查 0xF SPIN_LOCK_ALREADY_OWNED
description: SPIN_LOCK_ALREADY_OWNED bug 检查具有 0x0000000F 值。 这表示旋转锁的请求已启动的已拥有自旋锁时。
ms.assetid: 8347a78a-528e-4767-a13d-ad2fd8f71818
keywords:
- Bug 检查 0xF SPIN_LOCK_ALREADY_OWNED
- SPIN_LOCK_ALREADY_OWNED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SPIN_LOCK_ALREADY_OWNED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: af2c767441d8ed49a0bafc2551f37ca8292c8a1b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342101"
---
# <a name="bug-check-0xf-spinlockalreadyowned"></a>Bug 检查 0xF：旋转\_锁\_ALREADY\_拥有的


数值调节钮\_锁\_ALREADY\_拥有的 bug 检查的值为 0x0000000F。 这表示旋转锁的请求已启动的已拥有自旋锁时。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="spinlockalreadyowned-parameters"></a>旋转\_锁\_ALREADY\_拥有的参数


无

<a name="cause"></a>原因
-----

通常情况下，旋转锁的递归请求导致此错误。 如果类似于旋转锁的递归请求已启动-例如，当旋转锁已获取由一个线程，然后相同的线程调用的函数，还会尝试获得旋转锁时，它也可能发生。 第二个尝试获取旋转锁阻止不在此情况下，因为这样做可能会导致不可恢复的死锁。 如果调用对多个处理器，然后一个处理器之前将被阻止其他处理器释放锁。

此错误可以时也可能发生，而无需显式递归中，所有线程和所有自旋锁分配的 IRQL。 旋转锁于 Irql 始终是大于或等于 DPC 级别，但这不是线程，则返回 true。 但是，持有的自旋锁的线程必须保持 IRQL 大于或等于自旋锁。 减少线程下面 IRQL IRQL 它持有自旋锁级别允许另一个线程计划处理器上。 然后，此新线程可尝试获取同一个数值调节钮锁。

<a name="resolution"></a>分辨率
----------

请确保你不是以递归方式获取锁。 并保存旋转锁的线程，请确保你不会降低线程 IRQL 向下数值调节钮锁所占用的 IRQL 级别。

 

 




