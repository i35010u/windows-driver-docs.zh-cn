---
title: 获取 HDAUDIO_BUS_INTERFACE_V2 DDI 对象
description: 获取 HDAUDIO_BUS_INTERFACE_V2 DDI 对象
ms.assetid: 3aad8c7a-8c89-499a-bfe8-e3facdffcd15
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4710436e2fee9d4a827c03f4be372c214ed4d45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332268"
---
# <a name="obtaining-an-hdaudiobusinterfacev2-ddi-object"></a>获取 HDAUDIO\_总线\_接口\_V2 DDI 对象


下表显示了输入的参数值的函数驱动程序将写入到[ **IRP\_MN\_查询\_接口**](https://msdn.microsoft.com/library/windows/hardware/ff551687) IOCTL，以获取[**HDAUDIO\_总线\_界面\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)结构和版本的此结构定义 HD 音频 DDI 的上下文对象。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">ReplTest1</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>CONST GUID *<em>InterfaceType</em></p></td>
<td align="left"><p><strong>GUID_HDAUDIO_BUS_INTERFACE_V2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT<em>大小</em></p></td>
<td align="left"><p><strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff536418" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536418)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
</tr>
<tr class="odd">
<td align="left"><p>USHORT<em>版本</em></p></td>
<td align="left"><p>0x0100</p></td>
</tr>
<tr class="even">
<td align="left"><p>PINTERFACE<em>接口</em></p></td>
<td align="left"><p>指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff536418" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536418)"> <strong>HDAUDIO_BUS_INTERFACE_V2</strong> </a>结构</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PVOID <em>InterfaceSpecificData</em></p></td>
<td align="left"><p><strong>NULL</strong></p></td>
</tr>
</tbody>
</table>

 

功能驱动程序分配的存储[ **HDAUDIO\_总线\_接口\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)结构，并在 IOCTL 中包含指向此结构的指针。 在以前的表中，指向**HDAUDIO\_总线\_界面\_V2**结构转换为类型**PINTERFACE**，这是指向类型的结构的指针[**界面**](https://msdn.microsoft.com/library/windows/hardware/ff547825)。 名称和类型的前五个成员**HDAUDIO\_总线\_界面\_V2**匹配的五个成员**接口**。 **HDAUDIO\_总线\_界面\_V2**包含是 DDI 例程的函数指针的其他成员。 在响应功能驱动程序从接收 IOCTL，HD Audio 总线驱动程序填充**HDAUDIO\_总线\_界面\_V2**结构。

下表显示值 HD Audio 总线驱动程序将写入到的前五个成员[ **HDAUDIO\_总线\_接口\_V2** ](https://msdn.microsoft.com/library/windows/hardware/ff536418)结构。

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
<td align="left"><p><strong>sizeof</strong>(<a href="https://msdn.microsoft.com/library/windows/hardware/ff536418" data-raw-source="[&lt;strong&gt;HDAUDIO_BUS_INTERFACE_V2&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff536418)"><strong>HDAUDIO_BUS_INTERFACE_V2</strong></a>)</p></td>
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
<td align="left"><p>指向上下文对象的引用计数会递增的例程的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PINTERFACE_DEREFERENCE <strong>InterfaceDereference</strong></p></td>
<td align="left"><p>指向例程递减上下文对象的引用计数。</p></td>
</tr>
</tbody>
</table>

 

上表中**上下文**成员指向包含特定于基线 HD 音频 DDI 的特定实例的信息的上下文对象。 客户端从 IOCTL 获取此基线 HD 音频 DDI。 当客户端功能驱动程序调用的例程任何 DDI 中时，它必须始终指定**上下文**成员值作为第一个调用参数。 不透明的客户端的上下文信息。 HD Audio 总线驱动程序为每个客户端创建不同的上下文对象。 当不再需要的上下文对象时，客户端通过调用释放上下文对象**InterfaceDereference**例程上表中所示。 如果需要，客户端可以通过调用创建的对象的其他参考**InterfaceDereference**例程，但客户端负责释放这些引用，当不再需要它们。

 

 




