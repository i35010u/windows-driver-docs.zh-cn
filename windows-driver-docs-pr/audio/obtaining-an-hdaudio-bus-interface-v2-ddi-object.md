---
title: 获取 HDAUDIO_BUS_INTERFACE_V2 DDI 对象
description: 获取 HDAUDIO_BUS_INTERFACE_V2 DDI 对象
ms.assetid: 3aad8c7a-8c89-499a-bfe8-e3facdffcd15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9f726cdcc0e3dd1a08f0b000966f9c989880103
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830302"
---
# <a name="obtaining-an-hdaudio_bus_interface_v2-ddi-object"></a>获取 HDAUDIO\_总线\_接口\_V2 DDI 对象


下表显示了函数驱动程序写入[**IRP\_MN\_QUERY\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface)IOCTL 以获取[**HDAUDIO\_总线\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)结构和此结构定义的 HD 音频 DDI 版本的上下文对象。

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
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_V2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>大小</em></p></td>
<td align="left"><p><strong>sizeof</strong>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>版本</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>接口</em></p></td>
<td align="left"><p>指向<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>结构的指针</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>无效</strong></p></td>
</tr>
</tbody>
</table>

 

函数驱动程序为[**HDAUDIO\_总线\_接口\_V2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)结构分配存储，并在 IOCTL 中包含指向此结构的指针。 在上一个表中，指向**HDAUDIO\_总线\_接口\_V2**结构的指针被强制转换为类型**PINTERFACE**，这是指向类型[**接口**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)的结构的指针。 **HDAUDIO\_总线\_接口\_V2**的前五个成员的名称和类型与**接口**的五个成员的名称和类型匹配。 **HDAUDIO\_总线\_接口\_V2**包含其他成员，这些成员是指向 DDI 例程的函数指针。 为了响应从函数驱动程序接收 IOCTL，HD 音频总线驱动程序将填充**HDAUDIO\_总线\_接口\_V2**结构。

下表显示了高清音频总线驱动程序将 HDAUDIO 的前五个成员写入到[ **\_\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)的前五个成员的值\_V2 结构。

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
<td align="left"><p><strong>sizeof</strong>（<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/hdaudio/ns-hdaudio-_hdaudio_bus_interface_v2)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>）</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<strong>版本</strong></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID<strong>上下文</strong></p></td>
<td align="left"><p>必须作为第一个调用参数传递给每个 DDI 例程的上下文信息。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE_REFERENCE <strong>InterfaceReference</strong></p></td>
<td align="left"><p>指向用于递增上下文对象的引用计数的例程的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>指向一个例程的指针，该例程将减小上下文对象的引用计数。</p></td>
</tr>
</tbody>
</table>

 

在上表中，**上下文**成员指向上下文对象，该对象包含特定于基线 HD 音频 DDI 的特定实例的信息。 客户端从 IOCTL 获取此基线 HD 音频 DDI。 当客户端函数驱动程序调用 DDI 中的任何例程时，它必须始终将**上下文**成员值指定为第一个调用参数。 上下文信息对客户端是不透明的。 HD 音频总线驱动程序为每个客户端创建一个不同的上下文对象。 当不再需要上下文对象时，客户端将通过调用上表中显示的**InterfaceDereference**例程来释放上下文对象。 如果需要，客户端可以通过调用**InterfaceDereference**例程来创建对对象的其他引用，但当客户端不再需要这些引用时，该客户端负责将其释放。

 

 




