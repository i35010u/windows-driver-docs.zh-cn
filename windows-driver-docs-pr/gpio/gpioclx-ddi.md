---
title: GpioClx DDI
description: 常规用途 I/O (GPIO) 控制器驱动程序通过 GpioClx 设备驱动程序接口 (DDI) 与 GPIO 框架扩展 (GpioClx) 通信。
ms.assetid: AE8883C3-178F-44AB-AB1D-65DEC1472929
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67d762068cafa866ad2f4c7e3f9c9423b3c9f2de
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064470"
---
# <a name="gpioclx-ddi"></a>GpioClx DDI


常规用途 I/O (GPIO) 控制器驱动程序通过 GpioClx 设备驱动程序接口 (DDI) 与 GPIO 框架扩展 (GpioClx) 通信。 此 DDI 在 Gpioclx.h 头文件中定义，并在[常规用途 I/O (GPIO) 驱动程序参考](/windows-hardware/drivers/ddi/index)中进行了说明。 作为此 DDI 的一部分，GpioClx 实现多个[驱动程序支持方法](/previous-versions/hh439460(v=vs.85))，这些方法由 GPIO 控制器驱动程序调用。 此驱动程序实现了一组[事件回调函数](/previous-versions/hh439464(v=vs.85))，这些函数由 GpioClx 调用。 GpioClx 使用这些回调来管理已配置为中断输入的 GPIO 引脚提供的中断请求，并将数据传输到已配置为数据输入和输出的 GPIO 引脚，或者从其传输出来。

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
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/driver-support-methods-in-the-gpioclx-ddi" data-raw-source="[Driver Support Methods in the GpioClx DDI](./driver-support-methods-in-the-gpioclx-ddi.md)">GpioClx DDI 中的驱动程序支持方法</a></p></td>
<td><p>从 Windows 8 开始，使用 GPIO framework 扩展 (GpioClx) 。 GpioClx DDI 中系统提供的方法在 GpioClx 内核模式驱动程序中实现，Msgpioclx.sys。 此驱动程序为 <a href="https://docs.microsoft.com/previous-versions/hh439460(v=vs.85)" data-raw-source="[GpioClx driver support methods](/previous-versions/hh439460(v=vs.85))">GpioClx 驱动程序支持方法</a>导出入口点。 从 Windows 8 开始，Msgpioclx.sys 是操作系统的标准组件。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/optional-and-required-gpio-callback-functions" data-raw-source="[Optional and Required GPIO Callback Functions](./optional-and-required-gpio-callback-functions.md)">可选和必需的 GPIO 回调函数</a></p></td>
<td><p>常规用途 i/o (GPIO) 控制器驱动程序调用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient" data-raw-source="[&lt;strong&gt;GPIO_CLX_RegisterClient&lt;/strong&gt;](/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient)"><strong>GPIO_CLX_RegisterClient</strong></a> 方法，以注册为 GPIO framework 扩展的客户端 (GpioClx) 。 在此调用期间，驱动程序将注册数据包传递到 GpioClx，后者指定由驱动程序实现的事件回调函数的列表。 GpioClx 调用这些回调函数来配置 GPIO 控制器硬件、执行 i/o 操作和管理中断。 GpioClx 要求使用 GPIO 控制器驱动程序来实现某些回调函数，但对其他回调函数的支持是可选的。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/gpio-device-contexts" data-raw-source="[GPIO Device Contexts](./gpio-device-contexts.md)">GPIO 设备上下文</a></p></td>
<td><p>常规用途 i/o (GPIO) 控制器设备由框架设备对象表示。 GPIO 控制器驱动程序可以将设备上下文与此设备对象相关联。 驱动程序使用此设备上下文来持久存储有关 GPIO 控制器设备状态的信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/partitioning-a-gpio-controller-into-banks-of-pins" data-raw-source="[Partitioning a GPIO Controller into Banks of Pins](./partitioning-a-gpio-controller-into-banks-of-pins.md)">将 GPIO 控制器分区为管脚库</a></p></td>
<td><p>作为选项，驱动程序开发人员可以将常规用途 i/o 分区 (GPIO) 控制器设备分为两个或多个 GPIO 端口块。 例如，gpio 控制器驱动程序可以将具有 64 GPIO pin 的 GPIO 控制器设备描述为两个 bank，其中每个都具有 32 GPIO pin。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/gpio/implementation-issues-for-gpio-controller-drivers" data-raw-source="[Implementation Issues for GPIO Controller Drivers](./implementation-issues-for-gpio-controller-drivers.md)">GPIO 控制器驱动程序的实现问题</a></p></td>
<td><p>GPIO framework 扩展 (GpioClx) 提供 (DDI) 的灵活设备驱动程序接口。 此 DDI 使开发人员能够在备用回调接口之间进行选择。 驱动程序开发人员应该实现最适合目标 GPIO 控制器设备硬件体系结构的一组事件回调函数。</p></td>
</tr>
</tbody>
</table>

 

 

