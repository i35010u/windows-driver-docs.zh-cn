---
title: 特定于设备的方法 (_DSM)
description: 若要支持更多的功能和扩展来选择技术堆栈，Windows 设备定义特定于设备的方法 (_DSM)。
ms.assetid: E49BE897-28A5-42FE-875C-A8EB56EABF8B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78d49bb40956cca3c8312d8aec4bf6d109385b94
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328123"
---
# <a name="device-specific-methods-dsm"></a>特定于设备的方法 (\_DSM)


若要支持更多的功能和扩展来选择技术堆栈，Windows 定义了特定于设备的方法 (\_DSM) 设备。

[ACPI 5.0 规范](https://www.uefi.org/specifications)引入了 Windows 用于支持芯片 (SoC) 集成线路使用系统的硬件平台的多个特定于设备的方法。 在本部分中的主题描述了参数和返回值为这些方法定义。

## <a name="in-this-section"></a>本节内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>主题</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="gpio-controller-device-specific-method---dsm-.md" data-raw-source="[GPIO controller Device-Specific Method (_DSM)](gpio-controller-device-specific-method---dsm-.md)">GPIO 控制器特定于设备的方法 (_DSM)</a></p></td>
<td><p>若要支持各种特定于设备的类的 Windows 中的通用 I/O (GPIO) 驱动程序堆栈和平台固件之间的通信，Microsoft 定义了特定于设备的方法 (_DSM) 可以包含在 ACPI 中的 GPIO 控制器命名空间。</p></td>
</tr>
<tr class="even">
<td><p><a href="battery-device-specific-method.md" data-raw-source="[Battery Device-Specific Method](battery-device-specific-method.md)">电池特定于设备的方法</a></p></td>
<td><p>若要支持电池的被动热量管理平台，Microsoft 定义 _DSM 方法进行通信平台固件的散热限制由电池的散热区域设置的值。</p></td>
</tr>
<tr class="odd">
<td><p><a href="device-specific-method-for-microsoft-thermal-extensions.md" data-raw-source="[Device-Specific Method for Microsoft thermal extensions](device-specific-method-for-microsoft-thermal-extensions.md)">Microsoft 热量扩展的特定于设备的方法</a></p></td>
<td><p>若要支持的热量区域和温度传感器的更灵活的设计，Windows 支持扩展 ACPI 散热区域模型。 具体而言，Windows 对于每个热量区域支持的热量最小的中止值限制 (MTL)，还支持共享热量区域之间的温度传感器。</p></td>
</tr>
<tr class="even">
<td><p><a href="usb-device-specific-method---dsm-.md" data-raw-source="[USB Device-Specific Method (_DSM)](usb-device-specific-method---dsm-.md)">USB 设备特定的方法 (_DSM)</a></p></td>
<td><p>若要支持 USB 子系统的设备类特定配置，Windows 定义特定于设备的方法 (_DSM) 具有本文中介绍的函数。</p></td>
</tr>
<tr class="odd">
<td><p><a href="hidi2c-device-specific-method---dsm-.md" data-raw-source="[HIDI2C Device-Specific Method (_DSM)](hidi2c-device-specific-method---dsm-.md)">HIDI2C 特定于设备的方法 (_DSM)</a></p></td>
<td><p>部分 9.14.1，"_DSM （设备特定的方法）"，在中定义 _DSM 方法<a href="https://www.uefi.org/specifications" data-raw-source="[ACPI 5.0 specification](https://www.uefi.org/specifications)">ACPI 5.0 规范</a>。 此方法提供单个、 特定于设备的数据和控制功能可以无冲突其他此类特定于设备的方法调用的设备驱动程序。</p></td>
</tr>
<tr class="even">
<td><p><a href="windows-button-array-device-specific-method---dsm-.md" data-raw-source="[Windows button array Device-Specific Method (_DSM)](windows-button-array-device-specific-method---dsm-.md)">Windows 按钮数组特定于设备的方法 (_DSM)</a></p></td>
<td><p>若要支持的 Windows 按钮用户界面 (UI) 的发展，Windows 在本文中定义函数所述的 Windows 按钮数组设备特定于设备的方法 (_DSM)。</p></td>
</tr>
</tbody>
</table>

 

## <a name="other-dsms-defined-for-windows"></a>其他\_Dsm 定义 Windows


若要支持特定于设备的类的 Windows 中的驱动程序堆栈和平台固件之间的通信，Microsoft 定义了特定于设备的方法 (\_DSM) 与驱动程序一起使用。

|                                                                                                                                                                                             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 主题                                                                                                                                                                                       | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
| [\_字节可寻址能源的 DSM 接口支持的函数类 （函数接口 1）](https://msdn.microsoft.com/library/windows/hardware/mt604741) | \_字节可寻址能源支持的函数类 (函数接口 1) 的 DSM 接口设计为映射到 JEDEC 字节可寻址能源支持接口标准，以便最大程度减少 BIOS 复杂性。 它提供公共基础的报告设备功能和功能，以便操作系统软件可以通过相同的机制与各种实现交互。 此外，它允许对通过 I2C 寄存器访问特定于供应商的功能的支持。 |
| [\_针对 SATA 的 DSM （设备特定的方法）](https://msdn.microsoft.com/library/windows/hardware/dn613874)                                                                               | 此方法使您能够作为一个整体管理独立于主控制器的 SATA 控制器的每个端口。                                                                                                                                                                                                                                                                                                                                                                           |

 

 

 




