---
title: SPB 设备堆栈
description: Acpi.sys 为 SPB 上的外围设备创建 PDO。
ms.assetid: 21AB67A2-AA3C-4998-A532-78D6F6F76244
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16dc9c95a6f3fbb3e79b1566bd2c1f5c671b0c12
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734137"
---
# <a name="spb-device-stacks"></a>SPB 设备堆栈


Windows 驱动模型完全分离了用于控制外围设备的驱动程序组件 (例如，从管理总线控制器的驱动程序组件的总线上的温度传感器) ，后者可在外围设备之间传输数据和控制信息。 这种隔离使外设的硬件供应商能够连接到简单的 [外围总线](/previous-versions/hh450903(v=vs.85)) (SPB) 来编写驱动程序，该驱动程序可控制设备的各种总线控制器、总线类型和硬件平台。 同样，SPB 控制器的硬件供应商可以为此控制器写入一个驱动程序，该驱动程序可以启用到各种外围设备的连接。

在 Windows 中，连接到即插即用 (PnP) 总线的外围设备由两个或更多 *设备对象*表示。 *功能*设备对象 (FDO) 表示设备的内部状态，由控制外围设备内部功能的函数驱动程序创建和拥有。 堆栈中的 FDO 下是一个 (PDO) 的 *物理* 设备对象，表示设备与总线的连接。 PDO 由总线控制器驱动程序创建并拥有，该驱动程序检测并枚举 PnP 管理器的设备。 此 PDO 包含 (的信息，例如总线地址) 总线控制器通过总线访问设备所需的信息。 如果函数驱动程序需要总线控制器的帮助在设备上执行 i/o 操作，则函数驱动程序会将 i/o 请求数据包 (IRP 发送到 PDO) 设备堆栈，并且总线控制器驱动程序接收 IRP。 有关详细信息，请参阅 [设备对象和设备堆栈](../kernel/introduction-to-device-objects.md)。

与此相反，SPB (例如，I i2c 或 SPI 总线) 不支持 PnP，并且 SPB 控制器驱动程序不会检测和枚举 SPB 上的外围设备。 相反，硬件平台的 ACPI 固件介绍了这些设备及其总线连接，并且 Acpi.sys 的 ACPI 驱动程序为 PnP 管理器枚举这些设备。

此外，Acpi.sys 为 SPB 上的外围设备创建 PDO。 若要在此设备上执行 i/o 操作，设备的函数驱动程序不会将 IRP 发送到 PDO，因为 PDO 由 Acpi.sys 拥有，因此无法执行 i/o 操作。 相反，函数驱动程序必须将 IRP 发送到 SPB 控制器驱动程序。 SPB 控制器驱动程序拥有适用于 SPB 控制器的 FDO，该控制器与外围设备的 FDO 不在同一设备堆栈中。 若要发送此 IRP，设备的函数驱动程序必须首先打开到 SPB 控制器的逻辑连接，并接收此连接的 WDFFILEOBJECT 对象句柄。 然后，该驱动程序将此句柄指定为它发送到设备的 Irp 的目标。 SPB 控制器驱动程序接收这些 Irp 并 (与 [SPB framework 扩展](./spb-framework-extension.md)结合，SpbCx) 在设备上执行所需的 i/o 操作。 有关打开与 SPB 控制器的逻辑连接的详细信息，请参阅 [Spb 外围设备的连接 id](./connection-ids-for-spb-connected-peripheral-devices.md)。

某些 Irp 可以完全由 i/o 请求链中的 SPB 控制器驱动程序的驱动程序（包括外围设备的函数驱动程序）处理。 但是，必须由 SPB 控制器驱动程序处理需要将数据传输到外部设备和通过总线向外围设备传输数据或控制信息的 Irp。

设计为与 SPB 外围设备的函数驱动程序一起操作的筛选器驱动程序可以插入到函数驱动程序的 FDO 上。 但是，在 FDO 和 PDO 之间插入此类筛选器将不会产生任何影响，因为它无法截获在函数驱动程序与 SPB 控制器驱动程序之间交换的 Irp。

如有必要，可以将筛选器驱动程序插入到 SPB 控制器驱动程序 (和 SpbCx 上，该驱动程序管理发送到 SPB 控制器驱动程序) 的 Irp 的队列。 但是， [SPB i/o 请求接口](./using-the-spb-i-o-request-interface.md) 是顶级驱动程序接口，i/o 请求链中的驱动程序必须确保在调用线程的上下文中传递 i/o 请求，以便 SPBCX 和 SPB 控制器驱动程序可以在 i/o 传输过程中访问用户模式缓冲区。

