---
title: 使用系统的取消自旋锁
description: 使用系统的取消自旋锁
ms.assetid: dd3cf1e7-8ecc-4721-9160-86bf928687e4
keywords:
- 取消自旋锁 WDK 内核
- 数值调节钮锁 WDK 内核
- 系统取消自旋锁 WDK 内核
- STATUS_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de5d057827710875c458c933e3d7086e09e2d74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387002"
---
# <a name="using-the-systems-cancel-spin-lock"></a>使用系统的取消自旋锁





系统提供单个*取消自旋锁*，这是获取或释放某些系统例程调用时。

更改状态的可取消 Irp，包括所有可能的完成状态 IRP 的例程的驱动程序例程\_取消时，必须获取并释放系统取消自旋锁根据本部分中的准则。

驱动程序中的不是使用 I/O 管理器提供的设备队列，驱动程序的任何例程*取消*IRP 的可取消状态更改的例程必须首先调用[ **IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))获取系统取消自旋锁。

获取取消自旋锁可确保只有调用方可以更改该 IRP 的可取消状态。 I/O 管理器调用方持有旋转锁，而不能调用的驱动程序*取消*该 IRP 的例程。 同样，另一个驱动程序例程，如*DispatchCleanup*例程，不能同时尝试更改该 IRP 的可取消状态。

驱动程序例程不在驱动程序管理他们自己队列的 Irp 和驱动程序所提供的自旋锁用于同步访问队列，需要获取取消自旋锁之前，调用[ **IoSetCancelRoutine** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcancelroutine). 但是，这些驱动程序，应检查*取消*例程的指针的**IoSetCancelRoutine**返回以确定是否*取消*例程已启动。 请参阅[使用 Driver-Supplied 旋转锁](using-a-driver-supplied-spin-lock.md)有关详细信息。

调用的任何驱动程序例程**IoAcquireCancelSpinLock**必须调用**IoReleaseCancelSpinLock**越早越好。

驱动程序必须永远不会调用[ **IoCompleteRequest** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iocompleterequest)与同时保留数值调节钮锁定 IRP。 尝试在持有自旋锁完成 IRP，可能会导致死锁。

 

 




