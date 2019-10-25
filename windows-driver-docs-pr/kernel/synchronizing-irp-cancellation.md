---
title: 同步 IRP 取消
description: 同步 IRP 取消
ms.assetid: a110c6ad-794d-4b8a-a89d-bceb08ea82b8
keywords:
- 取消 Irp，同步
- 取消例程，同步
- 同步 WDK Irp
- 可取消的 Irp WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6780fe0356e005b2baaa25c6aebed83d2a4112c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836164"
---
# <a name="synchronizing-irp-cancellation"></a>同步 IRP 取消





从驱动程序的角度来看，IRP 可以随时取消。 IRP 取消异步发生;因此，如果在以下任何一点取消了 IRP，驱动程序必须能够处理许多潜在的争用条件：

-   在调用了驱动程序例程后，但在将 IRP 排队之前。

-   在调用了驱动程序例程之后但在尝试处理 IRP 之前。 例如，在调用驱动程序的[*StartIo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程后，但在*StartIo*例程从设备队列中删除 irp 之前，irp 可能会被取消。

-   当驱动程序例程取消排队 IRP 后，但在启动请求的 i/o 之前。

请注意，驱动程序将 IRP 排队并释放保护队列的任何自旋锁后，另一个线程可以访问和更改 IRP。 原始线程恢复时（即使是下一行代码），IRP 可能已被取消或更改。

驱动程序可以使用取消安全 IRP 队列框架来实现 IRP 队列。 然后，系统会为驱动程序注册一个可自动处理同步的[*取消*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_cancel)例程，以安全地取消 irp。 有关详细信息，请参阅[取消安全 IRP 队列](cancel-safe-irp-queues.md)。 否则，驱动程序必须实现自己的同步。

IRP 的以下成员包含有关取消的信息：

-   **Irp-&gt;"取消**" 指示 Irp 是否被取消或是否应取消。

-   **Irp-&gt;CancelRoutine**指示 Irp 是否可取消。 如果此成员包含指向 "取消" 例程的指针，则 IRP 可取消。 如果此成员为**NULL**，则 IRP 不可取消。 如果此成员为**NULL**，但设置了**Irp&gt;cancel** ，则表明取消例程正在运行并且 Irp 正在被取消。

如果驱动程序处理可取消的 Irp，它负责在其处于可取消状态的每个 IRP 中设置相应的*取消*例程。

本部分包括有关同步 IRP 取消的以下主题。

[使用系统的 Cancel 自旋锁](using-the-system-s-cancel-spin-lock.md)

[在处理 Irp 的驱动程序例程中同步取消](synchronizing-cancellation-in-driver-routines-that-process-irps.md)

[在没有取消例程的更高级别驱动程序中同步取消](synchronizing-cancellation-in-higher-level-drivers-without-cancel-rout.md)

[使用驱动程序提供的自旋锁](using-a-driver-supplied-spin-lock.md)

 

 




