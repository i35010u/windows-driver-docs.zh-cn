---
title: 监视器类功能驱动程序
description: 监视器类功能驱动程序
ms.assetid: d16c3dcc-2fbf-4579-8962-1b89e6e7b347
keywords:
- 多个监视器 WDK
- 监视类功能的驱动程序 WDK
- 函数的驱动程序 WDK 监视器
- 监视设备堆栈 WDK
- 设备堆栈 WDK 监视器
- 物理设备对象 WDK 监视器
- 功能的设备对象 WDK 监视器
- PDOs WDK 监视器
- FDOs WDK 监视器
- 筛选 DOs WDK 监视器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a46c032183e55f26c665f3e3bd40c2e6553e55a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545516"
---
# <a name="monitor-class-function-driver"></a>监视器类功能驱动程序


## <span id="ddk_monitor_class_function_driver_gg"></span><span id="DDK_MONITOR_CLASS_FUNCTION_DRIVER_GG"></span>


显示适配器的设备节点的子节点的设备节点表示具有连接到该监视器的显示适配器上每个视频输出。

通常情况下，有只有两个设备在设备堆栈中的对象表示的视频输出 (监视器） 对： 物理设备对象 (PDO) 和功能的设备对象 (FDO)。 在某些情况下，没有与供应商提供的筛选器驱动程序，上面 FDO 相关联的筛选器执行操作。 对于集成监视器，例如内置的平面面板的便携式计算机上，可能会与高级配置和电源接口 (ACPI) 驱动程序，上面 PDO 相关联的筛选器执行操作。

下表显示了已连接的监视器的视频输出设备堆栈。

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
<th align="left">驱动程序</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>筛选器执行操作</p></td>
<td align="left"><p>可选的通常不需要参数</p></td>
<td align="left"><p>由监视器供应商提供的筛选器驱动程序</p></td>
</tr>
<tr class="even">
<td align="left"><p>FDO</p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>监视类功能驱动程序 (Monitor.sys) 由 Microsoft 提供，</p></td>
</tr>
<tr class="odd">
<td align="left"><p>筛选器执行操作</p></td>
<td align="left"><p>仅需要集成 ACPI 显示面板</p></td>
<td align="left"><p>ACPI 驱动程序 (Acpi.sys) 由 Microsoft 提供，</p></td>
</tr>
<tr class="even">
<td align="left"><p>PDO</p></td>
<td align="left"><p>必需</p></td>
<td align="left"><p>总线驱动程序 （显示微型端口/端口对） 显示适配器供应商提供</p></td>
</tr>
</tbody>
</table>

 

用户模式应用程序使用 WMI 来调用服务的监视器类功能驱动程序。 这些服务包括公开监视器的标识数据和 （对于 ACPI 显示） 将设置显示器亮度。

监视器将其标识和功能的信息存储在一个扩展显示标识数据 (EDID) 结构，提供有关其标识和独立于通信的功能信息的主机的显示格式使用监视和主机之间的协议。 在用户模式应用程序，以在监视的设备堆栈中读取的监视器 EDID 处理功能驱动程序 (Monitor.sys) 的请求。 当监视器功能驱动程序收到请求，检索的监视器 EDID 时，它将请求发送到物理设备对象 (PDO) 表示的显示端口/微型端口驱动程序对在监视器的设备堆栈的底部。 显示端口/微型端口驱动程序对使用显示的数据通道 (DDC) 协议来读取的监视器 EDID I²C 总线，这是所有的标准监视器电缆中内置的简单两条总线。

可以使用获取 EDID [ACPI_METHOD_OUTPUT_DDC](https://docs.microsoft.com/windows-hardware/drivers/bringup/other-acpi-namespace-objects)方法中定义了其别名[Dispmprt.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dispmprt/)。 此方法是必需的而没有返回 EDID 数据的另一种标准机制集成 LCDs。

有关显示适配器与监视器之间的通信详细信息，请参阅以下主题：

[I2C 总线和子设备的显示适配器](i2c-bus-and-child-devices-of-the-display-adapter.md)

有关 EDID 结构和 DDC 协议的详细信息，请参阅以下标准已发布的视频电子标准协会 (VESA):

-   增强的显示数据通道标准 (E DDC)

-   增强的 EDID 标准 (E EDID)

您可以下载这些标准从[vesa.org](https://vesa.org/vesa-standards/)中*免费标准*部分。

有关 I²C 总线的详细信息，请参阅[I²C 总线规范](https://www.i2c-bus.org/specification/)Philips 半导体发布。

 

 





