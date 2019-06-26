---
title: 同步 IRP 取消
description: 同步 IRP 取消
ms.assetid: a110c6ad-794d-4b8a-a89d-bceb08ea82b8
keywords:
- 正在取消 Irp，同步
- 取消例程同步
- 同步 WDK Irp
- 可取消 Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8a5947725b86a7f4221a1e06d56d8f7e0e8b647e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355467"
---
# <a name="synchronizing-irp-cancellation"></a>同步 IRP 取消





从驱动程序的角度来看，可以在任何时候取消 IRP。 以异步方式; 发生 IRP 取消因此，驱动程序必须能够处理大量的潜在的争用情况，创建如果 IRP 取消在任何以下几点：

-   驱动程序例程调用之后，但队列 IRP 之前。

-   后一个驱动程序将调用例程，但之前尝试处理 IRP。 例如，IRP 的驱动程序后可能被取消[ *StartIo* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_startio)调用例程时，之前*StartIo*例程从设备队列中移除 IRP。

-   在驱动程序后例程取消排队 IRP，但它之前启动请求的 I/O。

请注意一个驱动程序排队 IRP，并释放任何保护该队列的自旋锁后，另一个线程可以访问和更改 IRP。 原始线程恢复的位置 — 甚至尽快下一行代码 — IRP 可能已被取消或否则更改。

驱动程序可以使用取消安全 IRP 队列框架实现 IRP 排队。 然后将系统[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_cancel)例程会自动处理同步，以便安全地取消 Irp 的驱动程序。 请参阅[取消安全 IRP 队列](cancel-safe-irp-queues.md)有关详细信息。 否则，驱动程序必须实现其自己的同步。

IRP 的以下成员包含有关取消的信息：

-   **Irp-&gt;取消**指示 IRP 正在取消还是应该取消。

-   **Irp-&gt;CancelRoutine**指示 IRP 是否可取消。 如果此成员包含在取消例程的指针，则可取消 IRP。 如果此成员是**NULL**，则 IRP 不是可取消。 如果此成员是**NULL**，但**Irp-&gt;取消**，则指示在取消例程运行和 IRP 正在被取消。

如果驱动程序处理可取消 Irp，它负责设置适当*取消*中处于可取消状态为每个 IRP 例程。

本部分包括有关同步 IRP 取消以下主题。

[使用系统的取消自旋锁](using-the-system-s-cancel-spin-lock.md)

[同步处理 Irp 的驱动程序例程中的取消操作](synchronizing-cancellation-in-driver-routines-that-process-irps.md)

[同步而无需取消例程的更高级别的驱动程序中的取消操作](synchronizing-cancellation-in-higher-level-drivers-without-cancel-rout.md)

[使用驱动程序所提供的旋转锁](using-a-driver-supplied-spin-lock.md)

 

 




