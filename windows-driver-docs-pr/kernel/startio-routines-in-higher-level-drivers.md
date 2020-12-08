---
title: 较高级驱动程序中的 StartIo 例程
description: 较高级驱动程序中的 StartIo 例程
keywords:
- StartIo 例程，更高级别的驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cbae8cd1b782e1be2025ecdf1fa1dc9e4dfce56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834395"
---
# <a name="startio-routines-in-higher-level-drivers"></a>较高级驱动程序中的 StartIo 例程





任何更高级别的驱动程序都可以具有 [*StartIo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程。 但是，此类驱动程序不太可能与现有的低级驱动程序互操作，并且可能会导致性能不佳。

较高级别的驱动程序中的 *StartIo* 例程具有以下效果：

-   可以通过从驱动程序的 *调度* Xxx 例程 (s) 和 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket) [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine)例程 () s 中调用 [**IoStartPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartpacket)来排队传入的 irp，从而导致每次通过 *StartIo* 例程处理一个 irp。

-   驱动程序的 i/o 吞吐量可能会明显减慢，因为它的 *StartIo* 例程可能会成为瓶颈。

-   驱动程序的 *StartIo* 例程会调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，其中每个 IRP 都以 IRQL 为间隔 = 调度 \_ 级别，从而导致所有较低级别的驱动程序的调度例程也以 irql = 调度 \_ 级别运行。 这限制了驱动程序可在其调度例程中调用的支持例程集。 由于大多数驱动程序编写器都假设其驱动程序的调度例程以 IRQL &lt; 调度 \_ 级别运行，因此较高级别的驱动程序不太可能与许多现有的低级驱动程序互操作。

-   *StartIo* 例程降低了整体系统吞吐量，因为它和其链中所有较低级别驱动程序的调度例程均以 IRQL = 调度 \_ 级别运行。

    有关运行标准驱动程序例程的 IRQLs 的详细信息，请参阅 [管理硬件优先级](managing-hardware-priorities.md)。

系统提供的高级驱动程序都不具有 *StartIo* 例程，因为它可能会减慢驱动程序本身的 IRP 处理，并对其上方和下方的所有驱动程序以及整体系统降低 IRP 处理速度。

大多数更高级别的驱动程序只需将 Irp 发送到其调度例程中的较低级别的驱动程序，并在其 *IoCompletion* 例程中执行任何必要的清理处理。

但是，更高级别的驱动程序可以为请求特定操作类型的 Irp 设置内部队列，或设置内部队列，以便为一组异类基础设备（如 SCSI 端口驱动程序）保存 Irp。 有关详细信息，请参阅对 [Irp 排队和出列](queuing-and-dequeuing-irps.md)。

 

