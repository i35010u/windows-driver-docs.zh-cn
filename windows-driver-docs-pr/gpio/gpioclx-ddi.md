---
title: GpioClx DDI
description: 常规用途 I/O (GPIO) 控制器驱动程序通过 GpioClx 设备驱动程序接口 (DDI) 与 GPIO 框架扩展 (GpioClx) 通信。
ms.assetid: AE8883C3-178F-44AB-AB1D-65DEC1472929
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff8a5283367f4ecebdd4de59308f4f42c264c815
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326133"
---
# <a name="gpioclx-ddi"></a>GpioClx DDI


常规用途 I/O (GPIO) 控制器驱动程序通过 GpioClx 设备驱动程序接口 (DDI) 与 GPIO 框架扩展 (GpioClx) 通信。 此 DDI 在 Gpioclx.h 头文件中定义，并在[常规用途 I/O (GPIO) 驱动程序参考](https://msdn.microsoft.com/library/windows/hardware/hh439515)中进行了说明。 作为此 DDI 的一部分，GpioClx 实现多个[驱动程序支持方法](https://msdn.microsoft.com/library/windows/hardware/hh439460)，这些方法由 GPIO 控制器驱动程序调用。 此驱动程序实现了一组[事件回调函数](https://msdn.microsoft.com/library/windows/hardware/hh439464)，这些函数由 GpioClx 调用。 GpioClx 使用这些回调来管理已配置为中断输入的 GPIO 引脚提供的中断请求，并将数据传输到已配置为数据输入和输出的 GPIO 引脚，或者从其传输出来。

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
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh439453" data-raw-source="[Driver Support Methods in the GpioClx DDI](https://msdn.microsoft.com/library/windows/hardware/hh439453)">GpioClx DDI 中的驱动程序支持方法</a></p></td>
<td><p>可从 Windows 8 开始 GPIO 框架扩展 (GpioClx)。 GpioClx 内核模式驱动程序 Msgpioclx.sys 中实现 GpioClx DDI 中系统提供的方法。 此驱动程序将导出的入口点<a href="https://msdn.microsoft.com/library/windows/hardware/hh439460" data-raw-source="[GpioClx driver support methods](https://msdn.microsoft.com/library/windows/hardware/hh439460)">GpioClx 驱动程序支持的方法</a>。 从 Windows 8 开始，Msgpioclx.sys 是操作系统的一个标准组件。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406514" data-raw-source="[Optional and Required GPIO Callback Functions](https://msdn.microsoft.com/library/windows/hardware/hh406514)">可选和必需 GPIO 回调函数</a></p></td>
<td><p>通用 I/O (GPIO) 控制器驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh439490" data-raw-source="[&lt;strong&gt;GPIO_CLX_RegisterClient&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439490)"> <strong>GPIO_CLX_RegisterClient</strong> </a>方法将注册为 GPIO 框架扩展 (GpioClx) 的客户端。 在此调用，驱动程序将注册数据包传递给 GpioClx 指定由驱动程序实现的事件回调函数的列表。 GpioClx 调用这些回调函数来配置 GPIO 控制器硬件、 执行 I/O 操作和管理中断。 GpioClx 需要 GPIO 控制器驱动程序，以实现特定的回调函数，但支持其他回调函数是可选的。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406460" data-raw-source="[GPIO Device Contexts](https://msdn.microsoft.com/library/windows/hardware/hh406460)">GPIO 设备上下文</a></p></td>
<td><p>常规用途的 I/O (GPIO) 控制器设备由 framework 设备对象表示。 GPIO 控制器驱动程序可以将此设备对象与关联的设备上下文。 驱动程序使用此设备上下文以永久存储 GPIO 控制器设备的状态信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406517" data-raw-source="[Partitioning a GPIO Controller into Banks of Pins](https://msdn.microsoft.com/library/windows/hardware/hh406517)">分区到银行引脚 GPIO 控制器</a></p></td>
<td><p>驱动程序开发人员可以，作为一个选项，分区到两个或多个银行的 GPIO 插针的通用 I/O (GPIO) 控制器设备。 例如，具有 64 GPIO 插针的 GPIO 控制器设备可以描述 GPIO 控制器驱动程序中，为两个银行，其中每个 32 GPIO 插针。</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/hh406479" data-raw-source="[Implementation Issues for GPIO Controller Drivers](https://msdn.microsoft.com/library/windows/hardware/hh406479)">GPIO 控制器驱动程序的实现问题</a></p></td>
<td><p>GPIO 框架扩展 (GpioClx) 提供了灵活的设备驱动程序接口 (DDI)。 此 DDI 使开发人员能够在备用回调接口之间进行选择。 驱动程序开发人员应实现最适合于目标 GPIO 控制器设备的硬件体系结构的事件回调函数集。</p></td>
</tr>
</tbody>
</table>

 

 

 




