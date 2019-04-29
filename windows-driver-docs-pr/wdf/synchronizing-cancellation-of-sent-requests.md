---
title: 将取消已发送请求的操作同步
description: 将取消已发送请求的操作同步
ms.assetid: e7ec65c9-bc7b-46ea-853d-3e23b1763666
keywords:
- 请求处理 WDK KMDF、 取消请求
- I/O 请求 WDK KMDF，取消
- 同步 WDK KMDF
- 请求处理 WDK KMDF，同步
- I/O 请求 WDK KMDF，同步
- 发送请求被取消 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39880b129b9f812fb276c6d19ec4404f6e40e8be
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376389"
---
# <a name="synchronizing-cancellation-of-sent-requests"></a>将取消已发送请求的操作同步


该驱动程序时驱动程序将尝试取消 I/O 请求它已转发给 I/O 目标，必须确保它可以通过有效的请求句柄[ **WdfRequestCancelSentRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff549941)方法。 请求句柄将变为无效如果 I/O 目标完成请求，因为在驱动程序[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数将调用[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945) （它会尝试删除请求对象）。

若要避免此问题，该驱动程序可以跟踪的已发送到 I/O 目标的例如，创建请求[集合](framework-object-collections.md)的请求对象。 该驱动程序可以调用[ **WdfSpinLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff550040)来同步对集合的访问。

当驱动程序的[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)调用回调函数，它将获取锁后，从该集合，并调用中删除已完成的请求的句柄[ **WdfSpinLockRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff550044)才能释放锁。

然后再尝试取消该驱动程序已转发给 I/O 目标的请求，该驱动程序可以：

1.  调用[ **WdfSpinLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff550040)获取自旋锁。

2.  在集合中查找请求对象的句柄，以确保该驱动程序完成例程尚未完成了请求并从集合中移除该句柄。

3.  调用[ **WdfObjectReference** ](https://msdn.microsoft.com/library/windows/hardware/ff548758)增加请求对象的引用计数，以便不能删除该对象。

4.  调用[ **WdfSpinLockRelease** ](https://msdn.microsoft.com/library/windows/hardware/ff550044)释放自旋锁。

5.  调用[ **WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)。

6.  调用[ **WdfObjectDereference** ](https://msdn.microsoft.com/library/windows/hardware/ff548739)以减少对象的引用计数。

此顺序可确保，如果 I/O 目标完成之前驱动程序调用请求[ **WdfRequestCancelSentRequest**](https://msdn.microsoft.com/library/windows/hardware/ff549941)，请求的句柄是否仍然有效 （由于递增引用计数），即使在驱动程序[ *CompletionRoutine* ](https://msdn.microsoft.com/library/windows/hardware/ff540745)回调函数调用[ **WdfRequestComplete**](https://msdn.microsoft.com/library/windows/hardware/ff549945)。

 

 





