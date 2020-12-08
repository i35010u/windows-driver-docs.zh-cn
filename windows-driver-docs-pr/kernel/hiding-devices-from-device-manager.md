---
title: 在设备管理器中隐藏设备
description: 在设备管理器中隐藏设备
keywords:
- 设备管理器 WDK，隐藏设备
- 设备 WDK，隐藏设备管理器
- 隐藏设备 WDK
- 隐藏设备 WDK
- NoDisplayClass 值 WDK 设备安装
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: edcf24be39f7f261801c242e507bbc4674bfd366
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817715"
---
# <a name="hiding-devices-from-device-manager"></a>在设备管理器中隐藏设备


默认情况下，设备管理器显示计算机上每个设备的状态。 在某些情况下，你可能想要阻止某些设备在设备管理器中出现。 例如，一个主板可能有一个 CardBus 控制器，该控制器的插槽不能由用户访问。 由于用户无法使用槽，因此不希望设备管理器显示有关设备的任何信息。

若要在设备管理器中隐藏某个设备，可以将该设备标记为 *隐藏的设备*。 通常，设备管理器不显示隐藏的设备。 但 (注意，用户可以覆盖此设置，并在设备管理器（甚至隐藏）中显示所有设备。 有关如何覆盖此设置的详细信息，请参阅 [查看隐藏的设备](../install/viewing-hidden-devices.md)。 ) 

可以通过两种方式将设备标记为隐藏：设备的驱动程序中或使用 ACPI BIOS。

### <a name="hiding-devices-from-within-a-driver"></a>从驱动程序中隐藏设备

驱动程序有两种方法可以将驱动程序标记为隐藏：

-   函数驱动程序或函数筛选器驱动程序可以通过响应 [**IRP \_ MN \_ 查询 \_ PNP \_ 设备 \_ 状态**](./irp-mn-query-pnp-device-state.md) IRP 来要求操作系统隐藏已成功启动的设备。 当 IRP 到达时，驱动程序必须将 PNP 设备设置为不会将 IoStatus 中的 \_ \_ \_ \_ UI 位显示在驱动程序的调度例程 **中** **。**

-   在 Windows XP 和更高版本的 Windows 操作系统上，总线驱动程序或总线筛选器驱动程序可以通过响应 [**irp \_ MN \_ 查询 \_ 功能**](./irp-mn-query-capabilities.md) irp，隐藏任何设备、启动或其他设备。 IRP 到达时，驱动程序必须将 **DeviceCapabilities. NoDisplayInUI** 成员设置为驱动程序的调度例程中的 **TRUE** 。 在某些情况下，总线筛选器驱动程序可能必须在完成例程中设置此位。 当基础总线驱动程序的调度例程错误地清除了其他驱动程序设置的所有功能字段时，需要执行此额外步骤。

### <a name="hiding-devices-by-using-the-acpi-bios"></a>使用 ACPI BIOS 隐藏设备

可以在 ACPI BIOS 中将设备标记为隐藏。 BIOS 可以 \_ 为设备公开 STA 方法。 \_STA 方法返回一个位掩码。 位 2 (掩码 0x4) 指定设备管理器是否应使设备在默认情况下可见。 如果应使设备可见，则此位应为 1; 否则为0。

例如，下面的代码示例演示如何隐藏根总线上的 USB 控制器。

```cpp
Device(PCI0) // Root PCI bus
_HID *PNP0A03 
...
    Device(UCTL)  // USB controller
    _ADR 0xddddffff // dddd = device, ffff = function
    _STA 0xB // Device present, but not shown
```

在 Microsoft Windows 2000 中，可以仅隐藏已启动的、工作的设备。 在 Windows XP 和更高版本的 Windows 中，还可以隐藏已损坏的设备。 由 STA 方法返回 (掩码 0x8) 的第三位 \_ 表明设备是否正常工作。 如果设备运行正常，则此位为 1; 否则为0。 例如，下面的代码示例演示了 BIOS 如何指示 USB 控制器断开并应隐藏：

```cpp
Device(PCI0) // Root PCI bus 
_HID *PNP0A03 
...
    Device(UCTL) // USB controller
    _ADR 0xddddffff //  dddd = device, ffff = function
    _STA 0x3 // Present, but broken and not shown 
```

**注意**   "解码" 位 (0x2) 与通过 ADR 方法描述的设备没有任何关联 \_ 。 前面的代码示例也可以在未设置解码位的情况下运行。 BIOS 编写器必须只跟踪通过 HID 方法描述的设备的解码状态 \_ 。

 

 

