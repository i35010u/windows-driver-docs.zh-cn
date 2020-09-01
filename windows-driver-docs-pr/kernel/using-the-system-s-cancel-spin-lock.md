---
title: 使用系统的取消自旋锁
description: 使用系统的取消自旋锁
ms.assetid: dd3cf1e7-8ecc-4721-9160-86bf928687e4
keywords:
- 取消旋转锁定 WDK 内核
- 旋转锁定 WDK 内核
- 系统取消自旋锁定 WDK 内核
- STATUS_CANCELLED
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e81c064c7dbde1cff4fb15b1f897a14fcc7cc272
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187699"
---
# <a name="using-the-systems-cancel-spin-lock"></a>使用系统的取消自旋锁





系统提供单个 *取消旋转锁*，在调用某些系统例程时获取或释放该锁。

更改可取消的 Irp 状态的驱动程序例程，其中包括所有可能完成状态为 "已取消" 的 IRP 的例程 \_ ，必须根据本部分中的准则获取并释放系统取消自旋锁。

在使用 i/o 管理器提供的设备队列的驱动程序中，任何更改 IRP 的 *可取消状态* 的其他驱动程序例程必须首先调用 [**IoAcquireCancelSpinLock**](/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) 以获取系统取消旋转锁。

获取 cancel 自旋锁可确保只有调用方可以更改该 IRP 的可取消状态。 当调用方持有自旋锁时，i/o 管理器无法调用该 IRP 的驱动程序 *取消* 例程。 同样，另一个驱动程序例程（如 *DispatchCleanup* 例程）无法同时尝试更改该 IRP 的可取消状态。

在管理其自己的 Irp 队列和使用驱动程序提供的自旋锁来同步队列访问的驱动程序中，在调用 [**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)之前，驱动程序例程无需获取 cancel 自旋锁。 但是，这些驱动程序应检查**IoSetCancelRoutine**返回的*取消*例程指针，以确定*取消*例程是否已启动。 有关详细信息，请参阅 [使用驱动程序提供的自旋锁](using-a-driver-supplied-spin-lock.md) 。

调用 **IoAcquireCancelSpinLock** 的任何驱动程序例程都必须尽快调用 **IoReleaseCancelSpinLock** 。

驱动程序在持有自旋锁时，决不能使用 IRP 调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。 尝试在持有自旋锁时完成 IRP 会导致死锁。

 

