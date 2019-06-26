---
title: 获取 HDAUDIO_BUS_INTERFACE_BDL DDI 对象
description: 获取 HDAUDIO_BUS_INTERFACE_BDL DDI 对象
ms.assetid: 142eb2f0-6c6d-4441-8ad7-0875546c1ab2
keywords:
- HDAUDIO_BUS_INTERFACE_BDL 结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50efee7a85e88e362dc9f591459350fed0d4516a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355346"
---
# <a name="obtaining-an-hdaudiobusinterfacebdl-ddi-object"></a>获取 HDAUDIO\_总线\_接口\_BDL DDI 对象


如上文所述，功能驱动程序的音频或调制解调器的编解码器通过发送获取对具有高清晰度音频 DDI 的对象的计数的引用[ **IRP\_MN\_查询\_接口** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IOCTL HD Audio 总线驱动程序。

下表显示了功能驱动程序将写入到 IOCTL，若要获取的输入的参数值[ **HDAUDIO\_总线\_接口\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构，此结构定义 HD 音频 DDI 的版本的上下文对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONST GUID *<em>InterfaceType</em></p></td>
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_BDL</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>大小</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>版本</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>接口</em></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"> <strong>HDAUDIO_BUS_INTERFACE_BDL</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

功能驱动程序分配的存储[ **HDAUDIO\_总线\_接口\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构，并在 IOCTL 中包含指向此结构的指针。 在前面的表中，指向**HDAUDIO\_总线\_界面\_BDL**结构转换为类型**PINTERFACE**，这是指向的结构的指针类型[**界面**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_interface)。 名称和类型的前五个成员**HDAUDIO\_总线\_界面\_BDL**匹配的五个成员**接口**。 **HDAUDIO\_总线\_界面\_BDL**包含是 DDI 例程的函数指针的其他成员。 在响应功能驱动程序从接收 IOCTL，HD Audio 总线驱动程序填充整个**HDAUDIO\_总线\_界面\_BDL**结构。

下表显示值 HD Audio 总线驱动程序将写入到的前五个成员[ **HDAUDIO\_总线\_接口\_BDL** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>USHORT<strong>大小</strong></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_BDL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hdaudio/ns-hdaudio-_hdaudio_bus_interface_bdl)"><strong>HDAUDIO_BUS_INTERFACE_BDL</strong></a>)</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>版本</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>上下文</strong></p></td>
<td align="left"><p>若要作为第一个调用参数传递给每个 DDI 例程所需的上下文信息</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>指向上下文对象的引用计数会递增的例程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>指向例程递减上下文对象的引用计数</p></td>
</tr>
</tbody>
</table>

 

在上表中，**上下文**成员将指向一个包含特定于 HDAUDIO 的特定实例的信息的上下文对象\_总线\_接口\_BDL 版本客户端获取从 IOCTL DDI。 如前所述，调用 DDI 中的任何例程时，客户端功能驱动程序必须始终指定**上下文**指针作为第一个调用参数的值。

 

 




