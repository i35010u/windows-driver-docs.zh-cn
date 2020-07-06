---
title: 特定于设备的方法（_DSM）
description: 为了支持增加的功能和扩展来选择技术堆栈，Windows 为设备定义了设备特定的方法（_DSM）。
ms.assetid: E49BE897-28A5-42FE-875C-A8EB56EABF8B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e9c304e3a406e33ded9a1fc90bf114405bb6579
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968048"
---
# <a name="device-specific-methods-_dsm"></a>特定于设备的方法（ \_ DSM）


为了支持增加的功能和扩展来选择技术堆栈，Windows 为设备定义了设备特定的方法（ \_ DSM）。

[ACPI 5.0 规范](https://uefi.org/specifications)介绍了几种特定于设备的方法，Windows 使用这些方法来支持在芯片（SoC）集成线路上使用系统的硬件平台。 本节中的主题介绍为这些方法定义的参数和返回值。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="gpio-controller-device-specific-method---dsm-.md" data-raw-source="[GPIO controller Device-Specific Method (_DSM)](gpio-controller-device-specific-method---dsm-.md)">GPIO 控制器的特定于设备的方法 (_DSM)</a></p></td>
<td><p>为了支持 Windows 和平台固件中的常规用途 i/o （GPIO）驱动程序堆栈之间的各种特定于设备类的通信，Microsoft 定义了一个特定于设备的方法（_DSM），该方法可包含在 ACPI 命名空间中的 GPIO 控制器下。</p></td>
</tr>
<tr class="even">
<td><p><a href="battery-device-specific-method.md" data-raw-source="[Battery Device-Specific Method](battery-device-specific-method.md)">电池的特定于设备的方法</a></p></td>
<td><p>为了支持平台被动热量管理，Microsoft 定义了一个 _DSM 方法，用于与平台固件通信，这是由电池的热区设置的温度限制。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-specific-method-for-microsoft-thermal-extensions.md" data-raw-source="[Device-Specific Method for Microsoft thermal extensions](device-specific-method-for-microsoft-thermal-extensions.md)">Microsoft 热量扩展的特定于设备的方法</a></p></td>
<td><p>为了支持更灵活的热区域和热传感器设计，Windows 支持向 ACPI 热区模型扩展。 具体而言，Windows 支持每个热区的热量最小限制（MTL），还支持在热量区域之间共享温度传感器。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-device-specific-method---dsm-.md" data-raw-source="[USB Device-Specific Method (_DSM)](usb-device-specific-method---dsm-.md)">USB 的特定于设备的方法 (_DSM)</a></p></td>
<td><p>为了支持 USB 子系统的设备特定于设备的配置，Windows 定义了一个特定于设备的方法（_DSM），其中包含本文所述的函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidi2c-device-specific-method---dsm-.md" data-raw-source="[HIDI2C Device-Specific Method (_DSM)](hidi2c-device-specific-method---dsm-.md)">HIDI2C 的特定于设备的方法 (_DSM)</a></p></td>
<td><p>_DSM 方法是在<a href="https://uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://uefi.org/specifications)">ACPI 5.0 规范</a>的 "_DSM （设备特定方法）" 部分中定义的。 此方法提供了特定于设备的数据和控制函数，可由设备驱动程序调用，而不会与其他此类特定于设备的方法发生冲突。</p></td>
</tr>
<tr class="even">
<td><p><a href="windows-button-array-device-specific-method---dsm-.md" data-raw-source="[Windows button array Device-Specific Method (_DSM)](windows-button-array-device-specific-method---dsm-.md)">Windows 按钮数组的特定于设备的方法 (_DSM)</a></p></td>
<td><p>为了支持 Windows 按钮用户界面（UI）的演变，Windows 为 Windows 按钮阵列设备定义了一种特定于设备的方法（_DSM），其中包含本文所述的函数。</p></td>
</tr>
</tbody>
</table>

 

## <a name="other-_dsms-defined-for-windows"></a>\_为 Windows 定义的其他 dsm


为了支持 Windows 中驱动程序堆栈和平台固件之间的设备特定于设备的通信，Microsoft 定义了 \_ 要用于驱动程序的设备特定方法（DSM）。

**主题**：说明

**[ \_ 用于字节寻址的支持能源的函数类的 DSM 接口（函数接口1）](https://docs.microsoft.com/windows-hardware/drivers/storage/-dsm-interface-for-byte-addressable-energy-backed-function-class--function-interface-1-)**： \_用于字节寻址的可获取能源支持的函数类（函数接口1）的 DSM 接口设计为映射到 它提供了报表设备功能 & 功能的常见基础，使 OS 软件可以通过相同的机制与各种实现交互。 此外，它还允许通过访问 I2C 寄存器来支持供应商特定的功能。

**[ \_ 适用于 sata 的 DSM （特定于设备的方法）](https://docs.microsoft.com/previous-versions/windows/hardware/design/dn613874(v=vs.85))**：通过此方法，可以将 sata 控制器的每个端口作为一个整体进行管理。


 

 

 




