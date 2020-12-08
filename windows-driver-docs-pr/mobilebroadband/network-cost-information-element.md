---
title: 网络成本信息元素
description: 网络成本信息元素
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6acd6a4c6678c513ae13db0bf5dc88ce2ea70e21
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805277"
---
# <a name="network-cost-information-element"></a>网络成本信息元素


为了将 Wi-Fi 网络的成本传达给客户端，Microsoft 已将供应商扩展定义为802.11 协议。 此扩展是网络成本 IE。

**注意**  
802.11 协议允许 (向) 供应商定义的信息元素，并要求不理解特定 IE 的客户端将其忽略并继续处理剩余的。 这可最大程度地降低将新的 IE 添加到与其他操作系统类型的现有客户端进行交互的产品的兼容性风险。

 

下表显示了网络开销 IE 格式：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>字段名称</th>
<th>大小 (八进制) </th>
<th>“值”</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>属性 ID</p></td>
<td><p>1</p></td>
<td><p>0xDD</p></td>
<td><p>键入 (供应商扩展) </p></td>
</tr>
<tr class="even">
<td><p>长度</p></td>
<td><p>1</p></td>
<td><p>0x08</p></td>
<td><p>以下字段的长度</p></td>
</tr>
<tr class="odd">
<td><p>按组织唯一标识符 (OUI) </p></td>
<td><p>3</p></td>
<td><p>0x00、0x50、0xF2</p></td>
<td><p>供应商 (Microsoft) </p></td>
</tr>
<tr class="even">
<td><p>OUI 类型</p></td>
<td><p>1</p></td>
<td><p>0X11</p></td>
<td><p>OUI 类型 (网络开销) </p></td>
</tr>
<tr class="odd">
<td><p>Cost 属性 (必需) </p></td>
<td><p>4</p></td>
<td><p>变量</p></td>
<td><p>DWORD，little endian 字节顺序</p></td>
</tr>
</tbody>
</table>

 

下图显示了 "开销" 属性字段的格式：

![设置成本属性字段的格式](images/fig1-mb-format-cost-attr-field.jpg)

下表显示了可能的成本级别位 (完全是必需的) ：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01</p></td>
<td><p>非受限</p></td>
<td><p>在此连接上传输数据时，不会产生任何增量成本。</p></td>
</tr>
<tr class="even">
<td><p>0x02</p></td>
<td><p>固定</p></td>
<td><p>数据传输按流量计量，并按数据限制进行计数。 此限制不会产生成本上的差异。</p></td>
</tr>
<tr class="odd">
<td><p>0x04</p></td>
<td><p>变量</p></td>
<td><p>此链接上的所有使用量都适用于增量成本。</p></td>
</tr>
</tbody>
</table>

 

下表显示了可能的成本标志位：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01 00 00</p></td>
<td><p>超过数据限制</p></td>
<td><p>使用量超出了数据的限制，并且应用了不同的网络成本或条件。</p></td>
</tr>
<tr class="even">
<td><p>0x02 00 00</p></td>
<td><p>Congested</p></td>
<td><p>网络运营商遇到或预期负载过大，请求减少了活动（如果可能）。</p></td>
</tr>
<tr class="odd">
<td><p>0x04 00 00</p></td>
<td><p>漫游</p></td>
<td><p>该连接在提供商的家庭网络外部漫游。</p></td>
</tr>
<tr class="even">
<td><p>0x08 00 00</p></td>
<td><p>接近数据限制</p></td>
<td><p>使用量接近数据限制;可能很快就会有不同的网络成本或情况。</p></td>
</tr>
</tbody>
</table>

 

下表显示了一些示例成本属性值：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>默认 WLAN</p></td>
<td><p>0x00 00 00 01</p></td>
<td><p>无限制连接;固定宽带支持的标准 WLAN。</p></td>
</tr>
<tr class="even">
<td><p>便携热点默认值</p></td>
<td><p>0x00 00 00 02</p></td>
<td><p>计量网络;限制未知或尚未达到;匹配移动宽带连接的 Windows 默认值。</p></td>
</tr>
<tr class="odd">
<td><p>超出限制/限制</p></td>
<td><p>0x00 01 00 01</p></td>
<td><p>用户已超出数据限制;速度降低，但没有其他使用限制。</p></td>
</tr>
<tr class="even">
<td><p>超出限制/费用</p></td>
<td><p>0x00 01 00 04</p></td>
<td><p>用户已超出数据限制;其他使用量会产生递增费用。</p></td>
</tr>
<tr class="odd">
<td><p>便携热点/漫游</p></td>
<td><p>0x00 04 00 04</p></td>
<td><p>连接是漫游的;由于网络状态，增加了费用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idadd_network_cost_support_to_your_devicespanspan-idadd_network_cost_support_to_your_devicespanspan-idadd_network_cost_support_to_your_devicespanadd-network-cost-support-to-your-device"></a><span id="Add_network_cost_support_to_your_device"></span><span id="add_network_cost_support_to_your_device"></span><span id="ADD_NETWORK_COST_SUPPORT_TO_YOUR_DEVICE"></span>向设备添加网络成本支持


1.  将 IE 添加到设备的 WLAN 信标和探测响应，该响应已固定到具有示例开销属性值的表中显示的 " **可移植热点" 默认** 值。 验证连接到此网络的 Windows 8、Windows 8.1 或 Windows 10 计算机是否自动为此网络选择 " **减少网络使用情况** " 选项。

2.  漫游时，将默认值替换为表中列出的 **可移植热点/漫游** 值以及示例成本属性值。

3.  （可选）使用合作伙伴运营商确定其他值可能适用的情况，如下所示：

    -   某些 bearers 时不受限制 (LTE、HSPA + 等 ) ，

    -   定义的通道检测超出限制状态。

    -   过去的数据限制时操作员定义的行为。

4.  （可选）如果你的设备可以将 Wi-Fi 用作第二跃点网络，请在连接的网络上检查此 IE，并将其值 (或其缺勤) 中继到你自己的 SSID。 如果不存在，请使用表中列出的 **默认 WLAN** 值以及示例成本属性值。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[通信通道](communication-channels.md)

 

 






