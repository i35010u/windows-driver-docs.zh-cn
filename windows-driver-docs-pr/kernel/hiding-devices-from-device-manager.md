---
title: 在设备管理器中隐藏设备
description: 在设备管理器中隐藏设备
ms.assetid: dd362ae1-ab14-44ee-982e-f972454c2623
keywords:
- 设备管理器 WDK，隐藏的设备
- 设备 WDK，隐藏从设备管理器
- 隐藏的设备 WDK
- 隐藏设备 WDK
- NoDisplayClass 值 WDK 设备安装
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ca217d09111a19bfc6cef8b81c677e0c321f6ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371879"
---
# <a name="hiding-devices-from-device-manager"></a>在设备管理器中隐藏设备


默认情况下，设备管理器的计算机上显示每个设备的状态。 在某些情况下，你可能想要阻止某些设备出现在设备管理器。 例如，主板可能包含不是用户可访问的槽的 CardBus 控制器。 用户不能使用该槽，因为您不希望设备管理器以显示有关设备的任何信息。

若要隐藏的设备在设备管理器，您可以将设备标记为*隐藏的设备*。 通常情况下，设备管理器不显示隐藏的设备。 （请注意，但是，用户可以重写此设置并显示在设备管理器中的所有设备，甚至是隐藏的。 有关如何重写此设置的详细信息，请参阅[查看隐藏的设备](https://docs.microsoft.com/windows-hardware/drivers/install/viewing-hidden-devices)。)

有两种方法，你将设备标记为隐藏： 内设备的驱动程序或通过使用 ACPI BIOS。

### <a name="hiding-devices-from-within-a-driver"></a>从驱动程序中的隐藏设备

驱动程序使用两种方法将标记为隐藏的驱动程序：

-   功能驱动程序或函数筛选器驱动程序可以请求通过响应隐藏已成功启动的设备的操作系统[ **IRP\_MN\_查询\_PNP\_设备\_状态**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-pnp-device-state) IRP。 当 IRP 到达时，该驱动程序必须设置 PNP\_设备\_不\_显示\_UI 中的位**IoStatus.Information**到**TRUE**中的驱动程序调度例程。

-   在 Windows XP 和更高版本的 Windows 操作系统，总线驱动程序或总线筛选器驱动程序可以隐藏任何设备、 启动或以其他方式，通过响应[ **IRP\_MN\_查询\_功能**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities) IRP。 当 IRP 到达时，必须设置驱动程序**Parameters.DeviceCapabilities.NoDisplayInUI**成员添加到**TRUE**驱动程序的调度例程中。 在某些情况下，总线筛选器驱动程序可能需要在完成例程中设置此位。 基础总线驱动程序的调度例程错误地清除其他驱动程序设置的所有功能字段时需要此额外步骤。

### <a name="hiding-devices-by-using-the-acpi-bios"></a>通过使用 ACPI BIOS 中隐藏的设备

可以将标记为隐藏在 ACPI BIOS 中的设备。 BIOS 可以公开\_设备 STA 方法。 \_STA 方法返回一个位掩码。 2 （掩码 0x4） 位指定是否设备管理器应使该设备显示默认情况下。 如果设备应将其变为可见和 0 否则，此位应为 1。

例如，以下代码示例演示如何在根总线上的 USB 控制器将处于隐藏状态。

```cpp
Device(PCI0) // Root PCI bus
_HID *PNP0A03 
...
    Device(UCTL)  // USB controller
    _ADR 0xddddffff // dddd = device, ffff = function
    _STA 0xB // Device present, but not shown
```

在 Microsoft Windows 2000 中，您可以隐藏仅开始，使用设备。 在 Windows XP 和更高版本的 Windows 中，您还可以隐藏断开的设备。 返回的位 3 （掩码 0x8） \_STA 方法指示设备是否正常工作。 如果设备正常工作，否则为 0，则此位为 1。 例如，下面的代码示例显示了如何将指示 BIOS，USB 控制器已断开，且应隐藏：

```cpp
Device(PCI0) // Root PCI bus 
_HID *PNP0A03 
...
    Device(UCTL) // USB controller
    _ADR 0xddddffff //  dddd = device, ffff = function
    _STA 0x3 // Present, but broken and not shown 
```

**请注意**  的"解码"位 (0x2) 没有任何关系的设备通过描述\_ADR 方法。 前面的代码示例还设置了解码位未工作。 BIOS 编写器必须跟踪仅适用于通过描述的设备的解码状态\_HID 方法。

 

 

 




