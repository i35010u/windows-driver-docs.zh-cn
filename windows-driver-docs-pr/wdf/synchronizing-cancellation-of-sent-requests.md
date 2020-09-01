---
title: 将取消已发送请求的操作同步
description: 将取消已发送请求的操作同步
ms.assetid: e7ec65c9-bc7b-46ea-853d-3e23b1763666
keywords:
- 请求处理 WDK KMDF，取消请求
- I/o 请求 WDK KMDF，取消
- 同步 WDK KMDF
- 请求处理 WDK KMDF，同步
- I/o 请求 WDK KMDF，同步
- 已发送请求取消 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c37408b7bbc7ce11c5ee579cee39e69cb9a30f75
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190745"
---
# <a name="synchronizing-cancellation-of-sent-requests"></a>将取消已发送请求的操作同步


当驱动程序尝试取消它已经转发到 i/o 目标的 i/o 请求时，该驱动程序必须确保它将有效的请求句柄传递到 [**WdfRequestCancelSentRequest**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest) 方法。 如果 i/o 目标完成了请求，则请求句柄无效，因为驱动程序的 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 回调函数将调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete) (这会尝试) 删除请求对象。

若要避免此问题，驱动程序可以跟踪它已发送到 i/o 目标的请求，例如，创建请求对象的 [集合](framework-object-collections.md) 。 驱动程序可以调用 [**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) 来同步对集合的访问。

当调用驱动程序的 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 回调函数时，它将获取该锁，从集合中移除已完成的请求的句柄，并调用 [**WdfSpinLockRelease**](/previous-versions/windows/hardware/drivers/ff550044(v=vs.85)) 以释放该锁。

在尝试取消驱动程序已转发到 i/o 目标的请求之前，驱动程序可以：

1.  调用 [**WdfSpinLockAcquire**](/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) 以获取旋转锁。

2.  在集合中查找请求对象的句柄，以确保驱动程序的完成例程没有完成请求，并从集合中删除了句柄。

3.  调用 [**WdfObjectReference**](./wdfobjectreference.md) 来递增请求对象的引用计数，以便无法删除该对象。

4.  调用 [**WdfSpinLockRelease**](/previous-versions/windows/hardware/drivers/ff550044(v=vs.85)) 以释放旋转锁定。

5.  调用 [**WdfRequestCancelSentRequest**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)。

6.  调用 [**WdfObjectDereference**](./wdfobjectdereference.md) 以减少对象的引用计数。

此顺序可确保在驱动程序调用 [**WdfRequestCancelSentRequest**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcancelsentrequest)之前 i/o 目标完成请求时，请求的句柄仍有效 (因为) 增加了引用计数，即使驱动程序的 [*CompletionRoutine*](/windows-hardware/drivers/ddi/wdfrequest/nc-wdfrequest-evt_wdf_request_completion_routine) 回调函数调用 [**WdfRequestComplete**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)也是如此。

 

