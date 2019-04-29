---
title: 适用于 WDF 驱动程序的 WDM 概念
description: 适用于 WDF 驱动程序的 WDM 概念
ms.assetid: 164b4882-a5a3-45d3-a2f5-53367b396439
keywords:
- 内核模式驱动程序 WDK KMDF WDM
- KMDF WDK WDM
- 内核模式驱动程序框架 WDK WDM
- 基于框架的驱动程序 WDK KMDF WDM
- WDM 驱动程序 WDK KMDF
- 总线枚举 WDK KMDF
- 总线驱动程序 WDK KMDF
- 函数的 WDK KMDF 驱动程序
- 筛选器驱动程序 WDK KMDF
- 驱动程序堆栈 WDK KMDF
- 堆栈 WDK KMDF
- 设备堆栈 WDK KMDF
- Irp WDK KMDF
- I/O 请求数据包 WDK KMDF
- I/O 请求 WDK KMDF Irp
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 70b117ebc4b00a809b0f2a12bce704410e4abdc8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385715"
---
# <a name="wdm-concepts-for-wdf-drivers"></a>适用于 WDF 驱动程序的 WDM 概念


Windows 驱动程序框架 (WDF) 是 Microsoft Windows 驱动程序模型 (WDM) 接口的包装。 尽管框架可简化许多 WDM 概念和完全隐藏其他人，以便不需要使用它们，但仍应了解一些 WDM 驱动程序的基本概念。 具体而言，您应该了解[驱动程序类型](#driver-types)，[驱动程序堆栈](#driver-stacks)，[设备堆栈](#device-stacks)，以及[I/O 请求数据包](#io-request-packets)。

### <a name="driver-types"></a>驱动程序类型

基于 Windows 的驱动程序被分到三种类型：[总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540704)，[函数的驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff546516)，并[筛选器驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff545890)。 总线驱动程序支持 I/O 总线通过检测插入到父总线子设备并报告它们的特征。 (此活动称为*总线枚举*。)功能的驱动程序控制设备和总线 I/O 的操作。 筛选器驱动程序接收，检查，并可能修改流之间用户应用程序和驱动程序，或单独的驱动程序之间的数据。

总线驱动程序实质上是函数的驱动程序还枚举子项。 驱动程序就像"总线驱动程序"时，它枚举子设备的总线上。 否则，相同的驱动程序"功能驱动程序"为总线时充当它处理访问总线适配器的硬件的 I/O 操作。

用户模式驱动程序框架 (UMDF) 驱动程序不能为总线驱动程序。

### <a name="driver-stacks"></a>驱动程序堆栈

在 Windows 操作系统，WDM 驱动程序中调用的垂直调用序列分层*驱动程序堆栈*。 堆栈中最顶层的驱动程序通常从用户应用程序，接收的 I/O 请求后通过操作系统的 I/O 管理器已传递请求。 较低的驱动程序层通常与计算机硬件进行通信。

简单的驱动程序堆栈提供堆栈，后者负责处理特定于总线的 I/O 操作并枚举子设备连接到它的底部总线驱动程序。 通常情况下，一个或多个特定于设备的功能的驱动程序是上面总线驱动程序。 这些功能的驱动程序处理连接到该总线的设备的 I/O 操作。 筛选器驱动程序可以是上述功能的驱动程序，也可以驻留在总线驱动程序和功能驱动程序之间。 正在运行的系统有多个支持不同类型的设备的驱动程序堆栈。

### <a name="device-stacks"></a>设备堆栈

每个驱动程序堆栈支持一个或多个*设备堆栈*。 设备堆栈是一套*设备对象*从 WDM 定义创建[**设备\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff543147)结构。 每个设备堆栈表示一台设备。 每个驱动程序为每个其设备创建设备对象并将每个设备对象附加到设备堆栈。 创建和删除，因为设备已插入和拔出，设备堆栈和每次重新启动系统。

当总线驱动程序检测到已接通电源或拔出子设备时，它会通知插即用 (PnP) 管理器。 在响应中，即插即用管理器对于每个连接到父设备 （即，总线） 的子设备要求总线驱动程序创建物理设备对象 (PDO)。 PDO 将成为设备堆栈的底部。

接下来，即插即用管理器加载函数和筛选器驱动程序以支持每个设备 （如果它们不是已加载），然后 PnP 管理器调用这些驱动程序，使每个可以创建一个设备对象并将其添加到设备堆栈的顶部。 功能的驱动程序创建功能的设备对象 (FDOs) 和筛选器驱动程序创建筛选器 （筛选 DOs） 的设备对象。

当 I/O 管理器将 I/O 请求发送到设备的驱动程序时，它将请求传递到驱动程序在设备堆栈中创建的最顶层的设备对象。 如果该驱动程序要求 I/O 管理器将请求传递到下一个较低的驱动程序，I/O 管理器将使用设备堆栈来确定下一步低驱动程序。 （下一步低驱动程序是创建的下一步下一个设备对象的驱动程序。）

WDF 创建每个 WDM 设备对象是 framework 的设备对象。 基于框架的驱动程序来访问这些框架设备对象而不是 WDM 设备对象。

### <a name="io-request-packets"></a>I/O 请求数据包

I/O 管理器将应用程序的 I/O 请求发送到驱动程序，通过创建 I/O 请求数据包 (Irp)。 IRP 可以包含执行 I/O 操作 （例如，读/写操作） 的请求或执行 I/O 控制 (IOCTL) 操作 （例如返回状态） 的请求。 此外，即插即用管理器创建表示 PnP Irp 和电源管理操作，必须执行驱动程序，然后发送这些 Irp 到驱动程序。

通常情况下，I/O 管理器创建读取或写入 IRP，当用户应用程序请求读取或写入操作。 I/O 管理器将 IRP 传递给驱动程序堆栈顶部的驱动程序，该驱动程序处理请求或将请求传递到下一个较低的驱动程序。 某些请求出差到堆栈的底部，并且完全处理某些更高级别的驱动程序。

驱动程序接收 IRP，每次该驱动程序还会收到指向表示必须处理该操作的设备的设备对象的指针。 因此，驱动程序堆栈中的驱动程序使用的设备对象来确定哪些他们插入中的设备特定的请求应转到。

WDF 驱动程序通常不直接访问 Irp。 该框架将为表示内核模式驱动程序框架 (KMDF) 和 UMDF 驱动程序接收的 I/O 队列中的框架请求对象的读取、 写入和设备 I/O 控制操作 WDM Irp。 Framework 句柄 PnP 和电源管理 Irp 在内部，并使用事件回调函数来通知电源事件和即插即用驱动程序。

 

 





