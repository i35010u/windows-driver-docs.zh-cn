---
title: 获取 HDAUDIO_BUS_INTERFACE_BDL DDI 对象
description: 获取 HDAUDIO_BUS_INTERFACE_BDL DDI 对象
ms.assetid: 142eb2f0-6c6d-4441-8ad7-0875546c1ab2
keywords:
- HDAUDIO_BUS_INTERFACE_BDL 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2531eac53ea9155fa46a45002aa11e31cfe1aa16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830307"
---
# <a name="obtaining-an-hdaudio_bus_interface_bdl-ddi-object"></a>获取 HDAUDIO\_总线\_接口\_BDL DDI 对象


如前文所述，音频或调制解调器编解码器的函数驱动程序通过将[**IRP\_MN\_查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)IOCTL 发送到 hd 音频总线驱动程序，获取对具有 HD 音频 DDI 的对象的计数引用。

下表显示了函数驱动程序向 IOCTL 中写入的输入参数值，以获取[**HDAUDIO\_总线\_接口\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构，以及此结构定义.

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONST GUID *<em>InterfaceType</em></p></td>
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_BDL</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>大小</em></p></td>
<td align="left"><p><strong>sizeof</strong>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>版本</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>接口</em></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>结构的指针</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>无效</strong></p></td>
</tr>
</tbody>
</table>

 

函数驱动程序为[**HDAUDIO\_总线\_接口\_BDL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构分配存储，并在 IOCTL 中包含指向此结构的指针。 在上表中，指向**HDAUDIO\_总线\_接口\_BDL**结构的指针被强制转换为类型**PINTERFACE**，这是指向类型[**接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)的结构的指针。 HDAUDIO 的前五个成员的名称和类型 **\_总线\_接口\_BDL**与这五个**接口**成员的名称和类型相匹配。 **HDAUDIO\_总线\_接口\_BDL**包含其他成员，这些成员是指向 DDI 例程的函数指针。 为了响应从函数驱动程序接收 IOCTL，HD 音频总线驱动程序将填充整个**HDAUDIO\_总线\_接口\_BDL**结构。

下表显示了高清音频总线驱动程序将 HDAUDIO 的前五个成员写入到[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)的前五个成员的值\_BDL 结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>USHORT<strong>大小</strong></p></td>
<td align="left"><p><strong>sizeof</strong>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>）</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>版本</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>上下文</strong></p></td>
<td align="left"><p>需要作为第一个调用参数传递给每个 DDI 例程的上下文信息</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>指向用于递增上下文对象的引用计数的例程的指针</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>指向一个例程的指针，该例程将减小上下文对象的引用计数</p></td>
</tr>
</tbody>
</table>

 

在上表中，**上下文**成员指向一个上下文对象，该对象包含特定于 HDAUDIO\_总线\_接口的特定实例的信息，\_客户端从IOCTL. 如前文所述，调用 DDI 中的任何例程时，客户端函数驱动程序必须始终将**上下文**指针值指定为第一个调用参数。

 

 




