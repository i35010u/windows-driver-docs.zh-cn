---
title: SPB 设备堆栈
description: Acpi.sys 存储上创建的是 PDO 外围设备。
ms.assetid: 21AB67A2-AA3C-4998-A532-78D6F6F76244
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22c17f477138ca7c750134f133f6fe8e37688258
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373387"
---
# <a name="spb-device-stacks"></a>SPB 设备堆栈


Windows 驱动程序模型完全分离开来控制外围设备 （例如，温度传感器） 的驱动程序组件的总线上管理来回传输数据和控制信息的总线控制器的驱动程序组件外围设备。 这种分离使连接到外围设备的硬件供应商[简单的外围总线](https://msdn.microsoft.com/library/windows/hardware/hh450903)（存储） 编写各种总线控制器、 总线类型和硬件平台的控制设备的驱动程序。 同样，存储控制器的硬件供应商可以为此可以启用连接到各种外围设备的控制器编写一个驱动程序。

在 Windows 中，附加到插即用 (PnP) 总线的外围设备用来表示两个，甚至可能更多，*设备对象*。 一个*功能*设备对象 (FDO) 表示内部状态的设备，以及是创建并拥有的功能驱动程序，用于控制外围设备的内部函数。 以下堆栈中 FDO*物理*表示设备已连接到总线的设备对象 (PDO)。 PDO 创建并拥有的用于检测和枚举即插即用管理器的设备的总线控制器驱动程序。 此 PDO 包含总线控制器需要通过总线访问设备的信息 （例如，总线地址）。 如果功能驱动程序需要从执行 I/O 操作在设备上的总线控制器的协助，功能驱动程序将向设备堆栈下的 I/O 请求数据包 (IRP) 发送到 PDO，和总线控制器驱动程序接收 IRP。 有关详细信息，请参阅[设备对象和设备堆栈](https://msdn.microsoft.com/library/windows/hardware/ff543153)。

与此相反，存储 （例如，I²C 或 SPI 总线） 不支持即插即用，并且存储控制器驱动程序不检测，枚举存储中的外围设备。 相反，硬件平台的 ACPI 固件介绍这些设备，并且其总线的连接，而 ACPI 驱动程序，Acpi.sys，枚举这些设备的即插即用的管理器。

此外，Acpi.sys 存储上创建的是 PDO 外围设备。 若要执行此设备上的 I/O 操作，设备的功能驱动程序不在堆栈的下层 IRP 向发送 PDO 因为 PDO 归 Acpi.sys，不能执行 I/O 操作。 相反，功能驱动程序必须将 IRP 发送到存储控制器驱动程序。 存储控制器驱动程序拥有存储控制器，它不在同一设备堆栈上为外围设备 FDO 的 FDO。 若要发送此 IRP，设备的功能驱动程序必须首先打开存储控制器的逻辑连接并接收到此连接的 WDFFILEOBJECT 对象句柄。 该驱动程序然后指定此句柄作为目标以 Irp 发送到设备。 存储控制器驱动程序将收到这些 Irp 和 (结合[存储框架扩展](https://msdn.microsoft.com/library/windows/hardware/hh406203)，SpbCx) 执行请求的 I/O 操作在设备上。 打开逻辑连接到存储控制器的详细信息，请参阅[存储外围设备的连接 Id](https://msdn.microsoft.com/library/windows/hardware/hh698216)。

某些 Irp 可以完全由上面 O 请求链，包括外围设备的功能驱动程序中的存储控制器驱动程序的驱动程序处理。 但是，Irp，需要传输到的数据或控件的信息，从外围设备通过总线必须处理由存储控制器驱动程序。

可以在函数驱动程序 FDO 的上方插入旨在与存储外围设备的功能驱动程序一起运行的筛选器驱动程序。 但是，插入 FDO 和 PDO 之间这样的筛选器不起因为它无法截获功能驱动程序和存储控制器驱动程序之间交换 Irp。

如有必要，可以更高版本的存储控制器驱动程序 （SpbCx，为 Irp 发送到存储控制器驱动程序管理的队列） 插入筛选器驱动程序。 但是，[存储 I/O 请求接口](https://msdn.microsoft.com/library/windows/hardware/hh698227)是顶级驱动程序接口，并且 O 请求链中的驱动程序必须确保将输入/输出请求传送的调用上下文中的线程，该 SpbCx 和存储控制器驱动程序可以在 I/O 传输过程中访问用户模式缓冲区。

 

 




