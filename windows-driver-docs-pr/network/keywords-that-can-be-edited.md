---
title: 可编辑的关键字
description: 可编辑的关键字
keywords:
- 安装关键字 WDK 网络，编辑
- 编辑安装关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a6003e497397c5583c6ef813906a9c66266cf4c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808609"
---
# <a name="keywords-that-can-be-edited"></a>可编辑的关键字





Ndis 6.0 和更高版本的 NDIS 提供可编辑网络设备的微型端口驱动程序的标准化关键字。 这些标准化关键字与可以在用户界面中编辑的数字或文本值相关联。

下面的示例演示了可以编辑的关键字的 INF 文件定义。

```INF
HKR, Ndi\params\<SubkeyName>,ParamDesc, 0, "<ParamDesc>"
HKR, Ndi\params\<SubkeyName>,Type, 0, "int"
HKR, Ndi\params\<SubkeyName>,Default, 0, "<IHV defined>"
HKR, Ndi\params\<SubkeyName>,Optional, 0, "0"
HKR, Ndi\params\<SubkeyName>,Min, 0, "0"
HKR, Ndi\params\<SubkeyName>,Max, 0, "<IHV defined>"
```

可以编辑的标准关键字包括：

<a href="" id="---------jumbopacket"></a>\*JumboPacket  
支持的最大巨型数据包的大小（以字节为单位） (一个大于1514字节的以太网帧) 硬件可以支持。 这也称为巨型帧。 *\* JumboPacket* 的值范围和最大值由 IHV 定义。 某些供应商允许其定义的最小值和最大值之间的任何值，而其他供应商则定义支持值的枚举。 有关详细信息，请与你的 IHV 联系。

<a href="" id="---------receivebuffers"></a>\*ReceiveBuffers  
微型端口适配器使用的接收描述符的数目。 微型端口驱动程序可以选择适用于性能优化的任何默认值。 请注意，如果值太小，微型端口适配器可能会在负载过重时用尽接收缓冲区。 如果值太大，则会浪费系统资源。

<a href="" id="---------transmitbuffers"></a>\*TransmitBuffers  
硬件可以支持的传输缓冲区的大小（以字节为单位）。 此大小与硬件相关，可以包含数据缓冲区、缓冲区描述符等。 硬件供应商可以分配适用于其用途的任何值。

<a href="" id="--------networkaddress"></a> Networkaddress.cache.ttl  
设备的网络地址。 MAC 地址的格式为： XX-XX-XX-xx-xx。 连字符 (-) 是可选的。

本主题末尾的表中的列描述了可编辑的关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定并且出现在注册表中的关键字的名称。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

<a href="" id="type"></a>类型  
可以编辑的值的类型。 该值可以是数字 (**Int**) ，也可以是可 (**Edit) 编辑** 的文本。

<a href="" id="default-value"></a>默认值  
整数或文本的默认值。 &lt;IHV 定义 &gt; 表示该值与特定的独立硬件供应商 (IHV) 要求相关联。

<a href="" id="min"></a>Min  
允许用于整数的最小值。 &lt;IHV 定义 &gt; 表示最小值与特定的 IHV 要求关联。

<a href="" id="max"></a>数量  
整数允许的最大值。 &lt;IHV 定义 &gt; 表示最小值与特定的 IHV 要求关联。

下表列出了所有关键字，并说明了驱动程序必须用于前面的特性的值。 有关关键字的详细信息，请在 WDK 文档中搜索关键字。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">类型</th>
<th align="left">默认值</th>
<th align="left">Min</th>
<th align="left">Max</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>JumboPacket</p></td>
<td align="left"><p>巨型数据包</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>1514</p></td>
<td align="left"><p>1514</p></td>
<td align="left"><p>&lt;已定义 IHV&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p></em>ReceiveBuffers</p></td>
<td align="left"><p>接收缓冲区</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>&lt;已定义 IHV&gt;</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>&lt;已定义 IHV&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>*TransmitBuffers</p></td>
<td align="left"><p>传输缓冲区</p></td>
<td align="left"><p>int</p></td>
<td align="left"><p>&lt;已定义 IHV&gt;</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>&lt;已定义 IHV&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>Networkaddress.cache.ttl</p></td>
<td align="left"><p>网络地址</p></td>
<td align="left"><p>编辑</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
</tr>
</tbody>
</table>

 

 

 





