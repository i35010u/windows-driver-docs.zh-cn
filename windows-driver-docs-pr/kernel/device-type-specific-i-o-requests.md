---
title: 特定于设备类型的 I/O 请求
description: 特定于设备类型的 I/O 请求
ms.assetid: 33ea0b0a-db58-40b7-b6d3-e981acf44dfe
keywords:
- Irp WDK 内核，特定于设备类型的 i/o 请求
- 特定于设备类型的 i/o 请求 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5d55a7fd1baef45ae1190102de826a636a2e8673
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838740"
---
# <a name="device-type-specific-io-requests"></a>特定于设备类型的 I/O 请求





Windows 驱动程序工具包（WDK）的特定于设备的部分提供有关由系统提供的、适用于最常见设备类型的驱动程序处理的特定于设备类型的 i/o 请求的信息。

如果新的驱动程序满足以下任一条件，则新的内核模式驱动程序必须处理与系统提供的驱动程序相同的 i/o 请求集：

-   新驱动程序将替换相同类型设备的系统驱动程序。

-   新驱动程序支持系统中已有的另一种类型的设备。

-   新驱动程序是中间（筛选器）驱动程序，在两个系统提供的驱动程序之间进行分层。

这种新的驱动程序必须处理系统提供的驱动程序处理的每个**IRP\_MJ\_* XXX*** 请求。 在大多数情况下，新的设备驱动程序还应处理[**IRP\_MJ\_设备\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-device-control)请求的相同**IOCTL\_* XXX*** 代码，即使新的驱动程序必须模拟相应系统提供的驱动程序。 否则，新的驱动程序可能会中断预计要接受这些类型请求的用户模式应用程序。

有关驱动程序可以在 Irp 的 i/o 状态块中设置的 NTSTATUS 值的信息，作为特定请求的返回值，请参阅[使用 NTSTATUS 值](using-ntstatus-values.md)。 有关可在错误日志数据包中指定的 NTSTATUS 值的信息，请参阅[日志记录错误](logging-errors.md)。 使用此信息来确定新的驱动程序要为类似类型的设备返回的相应状态值，或帮助确定驱动程序为新设备类型返回的相应状态值。

若要详细了解各种驱动程序以及每个驱动程序需要支持的请求，请参阅以下内容：

[串行设备和驱动程序](https://docs.microsoft.com/previous-versions/ff547451(v=vs.85))

[系统提供的并行驱动程序](https://docs.microsoft.com/previous-versions/ff544814(v=vs.85))

[存储驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-drivers)

[HID 体系结构](https://docs.microsoft.com/previous-versions/jj126193(v=vs.85))

[USB 客户端驱动程序的 i/o 请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#km-ioctl)

[IEEE 1394 驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/ieee/the-ieee-1394-driver-stack)

[访问 PCMCIA 设备的属性内存](https://docs.microsoft.com/windows-hardware/drivers/pcmcia/access-attribute-memory-of-a-pcmcia-device)

对于所有其他类型的驱动程序，请参阅文档以了解适当的驱动程序类型。

 

 




