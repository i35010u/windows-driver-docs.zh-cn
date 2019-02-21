---
title: 可编辑的关键字
description: 可编辑的关键字
ms.assetid: 88c3a285-941a-4c91-9e61-25c445d07344
keywords:
- 安装关键字 WDK 连接网络、 编辑
- 编辑安装关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa0be1bd273a620d252be35c452fa946550b99f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521637"
---
# <a name="keywords-that-can-be-edited"></a>可编辑的关键字





NDIS 6.0 和更高版本的 NDIS 网络设备的微型端口驱动程序提供可编辑的标准化的关键字。 这些标准化的关键字是可以编辑在用户界面中的数值或文本值与相关联。

下面的示例演示一个可编辑的关键字的 INF 文件定义。

```INF
HKR, Ndi\params\<SubkeyName>,ParamDesc, 0, "<ParamDesc>"
HKR, Ndi\params\<SubkeyName>,Type, 0, "int"
HKR, Ndi\params\<SubkeyName>,Default, 0, "<IHV defined>"
HKR, Ndi\params\<SubkeyName>,Optional, 0, "0"
HKR, Ndi\params\<SubkeyName>,Min, 0, "0"
HKR, Ndi\params\<SubkeyName>,Max, 0, "<IHV defined>"
```

可编辑的标准关键字是：

<a href="" id="---------jumbopacket"></a> \*JumboPacket  
支持的大小，以字节为单位的最大巨型数据包 （大于 1514 字节的以太网帧） 的硬件能够支持。 这也称为是 Jumbo 帧。 *\*JumboPacket*的值和最大值的范围是 IHV 定义。 某些供应商允许其定义最小值和最大值之间的任何值，而其他人定义支持的值的枚举。 有关详细信息，请与你 IHV。

<a href="" id="---------receivebuffers"></a> \*ReceiveBuffers  
描述符微型端口适配器所用的接收数。 微型端口驱动程序可以选择任何适用的默认值以进行性能优化。 请注意，是否值太小，微型端口适配器可能会用完负载过大的接收缓冲区。 如果值太大，就会浪费掉系统资源。

<a href="" id="---------transmitbuffers"></a> \*TransmitBuffers  
以字节为单位的硬件能够支持的传输缓冲区的大小。 此大小取决于硬件，可以包括数据缓冲区、 缓冲区描述符等。 硬件供应商可以分配适用于它们的用途的任何值。

<a href="" id="--------networkaddress"></a> NetworkAddress  
设备的网络地址。 MAC 地址的格式为：XX-XX-XX-XX-XX-XX. 连字符 （-） 是可选的。

本主题末尾处表中的列描述关键字，可以编辑以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须指定 INF 文件中的关键字的名称显示在注册表中。

<a href="" id="paramdesc"></a>ParamDesc  
显示文本与 SubkeyName 相关联。

<a href="" id="type"></a>Type  
可编辑的值的类型。 值可以是数字 (**Int**) 或可以编辑的文本 (**编辑**)。

<a href="" id="default-value"></a>默认值  
整数或文本的默认值。 &lt;IHV 定义&gt;指示的值是与特定的独立硬件供应商 (IHV) 要求相关联。

<a href="" id="min"></a>最小值  
允许整数的最小值。 &lt;IHV 定义&gt;表示的最小值与特定的 IHV 要求相关联。

<a href="" id="max"></a>最大值  
允许整数的最大值。 &lt;IHV 定义&gt;表示的最小值与特定的 IHV 要求相关联。

下表列出的所有关键字，并说明了一个驱动程序必须用于对上述属性的值。 有关关键字的详细信息，搜索 WDK 文档中的关键字。

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
<th align="left">在任务栏的搜索框中键入</th>
<th align="left">默认值</th>
<th align="left">最小</th>
<th align="left">最大</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>JumboPacket</p></td>
<td align="left"><p>极大的数据包</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>1514</p></td>
<td align="left"><p>1514</p></td>
<td align="left"><p>&lt;IHV 定义&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p></em>ReceiveBuffers</p></td>
<td align="left"><p>接收缓冲区</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>&lt;IHV 定义&gt;</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>&lt;IHV 定义&gt;</p></td>
</tr>
<tr class="odd">
<td align="left"><p>*TransmitBuffers</p></td>
<td align="left"><p>传输缓冲区</p></td>
<td align="left"><p>整型</p></td>
<td align="left"><p>&lt;IHV 定义&gt;</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>&lt;IHV 定义&gt;</p></td>
</tr>
<tr class="even">
<td align="left"><p>NetworkAddress</p></td>
<td align="left"><p>网络地址</p></td>
<td align="left"><p>编辑</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>不适用</p></td>
</tr>
</tbody>
</table>

 

 

 





