---
title: Bug 检查 0xF SPIN_LOCK_ALREADY_OWNED
description: SPIN_LOCK_ALREADY_OWNED bug 检查的值为0x0000000F。 这表示在已经拥有自旋锁时，已启动了自旋锁请求。
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
ms.openlocfilehash: eb831258764990428d984fc3dedd7fea096a317b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836893"
---
# <a name="bug-check-0xf-spin_lock_already_owned"></a>Bug 检查0xF： \_ \_ 已拥有自旋 \_ 锁


自旋 \_ 锁 \_ 已 \_ 拥有 bug 检查的值为0x0000000F。 这表示在已经拥有自旋锁时，已启动了自旋锁请求。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="spin_lock_already_owned-parameters"></a>旋转 \_ 锁 \_ 已 \_ 拥有参数


无

<a name="cause"></a>原因
-----

通常，此错误是由对自旋锁的递归请求引起的。 如果已经启动了类似于自旋锁的递归请求的内容，则可能发生此情况，例如，当线程获取了自旋锁，然后该同一线程调用函数时，也会尝试获取旋转锁。 在这种情况下，不会阻止第二次获取自旋锁的尝试，因为这样做会导致无法恢复的死锁。 如果对多个处理器进行调用，则在其他处理器释放该锁之前，将阻止一个处理器。

如果对所有线程和所有自旋锁都分配了 IRQL，则此错误也可能发生（没有显式递归）。 旋转锁定 IRQLs 始终大于或等于 DPC 级别，但对于线程，这种情况并不适用。 但是，持有自旋锁的线程必须保持大于或等于自旋锁的 IRQL。 将线程 IRQL 减小到它所持有的自旋锁的 IRQL 级别下面可在处理器上计划另一个线程。 然后，此新线程可以尝试获取同一自旋锁。

<a name="resolution"></a>解决方法
----------

确保不以递归方式获取锁。 对于持有自旋锁的线程，请确保不将线程 IRQL 减小到其所持有的自旋锁的 IRQL 以下的级别。

 

 




