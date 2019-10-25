---
title: 监视类函数驱动程序
description: 监视类函数驱动程序
ms.assetid: d16c3dcc-2fbf-4579-8962-1b89e6e7b347
keywords:
- 多监视器 WDK
- 监视类函数驱动程序 WDK
- 函数驱动程序 WDK 监视器
- 监视设备堆栈 WDK
- 设备堆栈 WDK 监视器
- 物理设备对象 WDK 监视器
- 功能设备对象 WDK 监视器
- PDOs WDK 监视器
- FDOs WDK 监视器
- 筛选 DOs WDK 监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e46a9ade660ea960ef7c447b6ee8dbbba321906
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840559"
---
# <a name="monitor-class-function-driver"></a>监视类函数驱动程序


## <span id="ddk_monitor_class_function_driver_gg"></span><span id="DDK_MONITOR_CLASS_FUNCTION_DRIVER_GG"></span>


显示适配器上连接了监视器的每个视频输出都由一个设备节点表示，该节点是显示适配器的设备节点的子节点。

通常，设备堆栈中只有两个设备对象表示（视频输出、监视器）对：物理设备对象（PDO）和功能设备对象（FDO）。 在某些情况下，具有与供应商提供的筛选器驱动程序相关联的筛选器（FDO）。 对于集成的监视器（如便携式计算机上的内置平板面板），可能存在一个与 PDO 上的高级配置和电源接口（ACPI）驱动程序相关联的筛选器。

下表显示了具有连接的监视器的视频输出的设备堆栈。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">设备对象</th>
<th align="left">必需/可选</th>
<th align="left">“驱动程序”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>筛选器 DO</p></td>
<td align="left"><p>可选，通常不需要</p></td>
<td align="left"><p>监视供应商提供的筛选器驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>FDO</p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>Microsoft 提供的监视类函数驱动程序（Monitor）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>筛选器 DO</p></td>
<td align="left"><p>仅适用于集成 ACPI 显示面板的要求</p></td>
<td align="left"><p>Microsoft 提供的 ACPI 驱动程序（Acpi）</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDO</p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>显示适配器供应商提供的总线驱动程序（显示微型端口/端口对）</p></td>
</tr>
</tbody>
</table>

 

用户模式应用程序使用 WMI 来调用 monitor 类函数驱动程序的服务。 这些服务包括公开监视器的标识数据，并在使用 ACPI 显示时设置显示亮度。

监视器将其标识和功能信息存储在扩展的显示标识数据（EDID）结构中，这种格式允许显示为主机提供其标识和功能的相关信息，而不依赖于通信监视器和主机之间使用的协议。 用户模式应用程序发出的用于读取监视器 EDID 的请求会由该监视器的设备堆栈中的函数驱动程序（sys.databases）处理。 当监视器函数驱动程序收到检索监视器 EDID 的请求时，它会将请求发送到显示器设备堆栈底部的物理设备对象（PDO）表示的显示端口/微型端口驱动程序对。 显示端口/微型端口驱动程序对使用显示数据通道（DDC）协议在 I i2c 总线上读取监视器的 EDID，此总线是内置于所有标准监视器电缆的简单双线总线。

可以使用[ACPI_METHOD_OUTPUT_DDC](https://docs.microsoft.com/windows-hardware/drivers/bringup/other-acpi-namespace-objects)方法获取 EDID，其别名在[Dispmprt](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/)中定义。 此方法对于没有其他标准机制来返回 EDID 数据的集成 Lcd 是必需的。

有关显示适配器与监视器之间通信的详细信息，请参阅以下主题：

[显示适配器的 I2C 总线和子设备](i2c-bus-and-child-devices-of-the-display-adapter.md)

有关 EDID 结构和 DDC 协议的详细信息，请参阅视频电子标准协会（VESA）发布的以下标准：

-   增强的显示数据通道标准（E-DDC）

-   增强的 EDID 标准（E-EDID）

可以从 "*免费标准*" 部分的[vesa.org](https://vesa.org/vesa-standards/)下载这些标准。

有关 I i2c 总线的详细信息，请参阅由 Philips 半导体发布的[i I2c 总线规范](https://www.i2c-bus.org/specification/)。

 

 





