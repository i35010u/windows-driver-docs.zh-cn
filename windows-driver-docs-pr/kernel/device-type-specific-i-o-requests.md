---
title: 特定于设备类型的 I/O 请求
description: 特定于设备类型的 I/O 请求
ms.assetid: 33ea0b0a-db58-40b7-b6d3-e981acf44dfe
keywords:
- Irp WDK 内核，设备特定于类型的 I/O 请求
- 设备特定于类型的 I/O 请求 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: df29a43a770745e35576b771c05f6e64e2cf973d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562133"
---
# <a name="device-type-specific-io-requests"></a>特定于设备类型的 I/O 请求





特定于设备的部分的 Windows Driver Kit (WDK) 提供有关设备特定于类型的 I/O 请求处理的最常见类型的设备的系统提供的驱动程序的信息。

如果新的驱动程序符合以下条件的任何新的内核模式驱动程序必须处理系统提供的驱动程序相同的输入/输出请求集：

-   新的驱动程序将替换相同类型的设备的系统驱动程序。

-   新的驱动程序支持已在系统中的一种类型的另一台设备。

-   新的驱动程序是一个分层两个系统提供驱动程序之间的中间 （筛选器） 驱动程序。

此类新的驱动程序必须处理每个**IRP\_MJ\_* XXX*** 的系统提供的驱动程序处理的请求。 在大多数情况下，新的设备驱动程序还应处理同一套**IOCTL\_* XXX*** 代码[ **IRP\_MJ\_设备\_控件**](https://msdn.microsoft.com/library/windows/hardware/ff550744)请求时，即使新的驱动程序必须模拟相应的系统提供的驱动程序的行为。 否则，新的驱动程序可能会破坏这些类型的请求会始终期待的用户模式应用程序。

有关驱动程序的 Irp，I/O 状态块中可设置为特定请求的返回值的 NTSTATUS 值的信息，请参阅[使用 NTSTATUS 值](using-ntstatus-values.md)。 可指定在错误日志包中的 NTSTATUS 值有关的信息，请参阅[日志记录错误](logging-errors.md)。 使用此信息来对相应的状态的值决定要返回的相似类型的设备，或以帮助确定相应的状态值要返回的是新类型的设备的驱动程序的新驱动程序。

有关各种类型的驱动程序和每个都是需要支持的请求的详细信息，请参阅：

[串行设备和驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff547451)

[系统提供的并行驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff544814)

[存储驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff566976)

[HID 体系结构](https://msdn.microsoft.com/library/windows/hardware/jj126193)

[USB 客户端驱动程序的 I/O 请求](https://msdn.microsoft.com/library/windows/hardware/ff540134#km-ioctl)

[IEEE 1394 驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/ff538867)

[访问 PCMCIA 设备的属性内存](https://msdn.microsoft.com/library/windows/hardware/ff536892)

对于所有其他类型的驱动程序，请参考相应的驱动程序类型的文档。

 

 




