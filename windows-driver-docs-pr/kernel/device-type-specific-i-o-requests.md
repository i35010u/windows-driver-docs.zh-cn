---
title: 特定于设备类型的 I/O 请求
description: 特定于设备类型的 I/O 请求
keywords:
- Irp WDK 内核，特定于设备类型的 i/o 请求
- 特定于设备类型的 i/o 请求 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2220d8de9b3cb89c95a72eed4bc1ea09f0a62fbc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792791"
---
# <a name="device-type-specific-io-requests"></a>特定于设备类型的 I/O 请求





Windows 驱动程序工具包 (WDK) 的特定于设备的部分，提供有关由系统提供的、适用于最常见设备类型的驱动程序处理的特定于设备类型的 i/o 请求的信息。

如果新的驱动程序满足以下任一条件，则新的内核模式驱动程序必须处理与系统提供的驱动程序相同的 i/o 请求集：

-   新驱动程序将替换相同类型设备的系统驱动程序。

-   新驱动程序支持系统中已有的另一种类型的设备。

-   新的驱动程序是一个中间 (筛选器) 驱动程序，在两个系统提供的驱动程序之间进行分层。

此类新驱动程序必须处理系统提供的驱动程序处理的每个 **IRP \_ MJ \_ * XXX*** 请求。 在大多数情况下，新的设备驱动程序还应处理 [**IRP \_ MJ \_ 设备 \_ 控制**](./irp-mj-device-control.md)请求的相同 **IOCTL \_ * XXX*** 代码集，即使新的驱动程序必须模拟相应系统提供的驱动程序的行为。 否则，新的驱动程序可能会中断预计要接受这些类型请求的用户模式应用程序。

有关驱动程序可以在 Irp 的 i/o 状态块中设置的 NTSTATUS 值的信息，作为特定请求的返回值，请参阅 [使用 NTSTATUS 值](using-ntstatus-values.md)。 有关可在错误日志数据包中指定的 NTSTATUS 值的信息，请参阅 [日志记录错误](logging-errors.md)。 使用此信息来确定新的驱动程序要为类似类型的设备返回的相应状态值，或帮助确定驱动程序为新设备类型返回的相应状态值。

若要详细了解各种驱动程序以及每个驱动程序需要支持的请求，请参阅以下内容：

[串行设备和驱动程序](../serports/using-serial-sys-and-serenum-sys.md)

[系统提供的并行驱动程序](../parports/system-supplied-parallel-drivers.md)

[存储驱动程序](../storage/storage-drivers.md)

[HID 体系结构](../hid/hid-architecture.md)

[USB 客户端驱动程序的 i/o 请求](/windows-hardware/drivers/ddi/_usbref/#km-ioctl)

[IEEE 1394 驱动程序堆栈](../ieee/the-ieee-1394-driver-stack.md)

[访问 PCMCIA 设备的属性内存](../pcmcia/access-attribute-memory-of-a-pcmcia-device.md)

对于所有其他类型的驱动程序，请参阅文档以了解适当的驱动程序类型。

