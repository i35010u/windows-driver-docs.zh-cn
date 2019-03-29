---
title: 网络成本信息元素
description: 网络成本信息元素
ms.assetid: 973294b5-0c4f-4056-ad28-62c58f10c232
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 347344b72f12e246ce633ec58f8f5cde5612d929
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563188"
---
# <a name="network-cost-information-element"></a>网络成本信息元素


若要向客户端通信的 Wi-fi 网络的成本，Microsoft 还为 802.11 协议定义供应商扩展。 此扩展是网络成本 IE。

**请注意**   802.11 协议允许供应商定义的信息元素 (IEs)，所需的不了解特定的 IE，若要将其忽略并继续处理剩余导致浏览器客户端。 添加新的 IE 进行交互的产品与其他操作系统类型的现有客户端的兼容性风险降至最低。

 

下表显示了网络成本 IE 格式：

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
<th>大小 （八进制）</th>
<th>值</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>属性 ID</p></td>
<td><p>1</p></td>
<td><p>0xDD</p></td>
<td><p>类型 （供应商扩展）</p></td>
</tr>
<tr class="even">
<td><p>长度</p></td>
<td><p>1</p></td>
<td><p>0x08</p></td>
<td><p>以下字段的长度</p></td>
</tr>
<tr class="odd">
<td><p>组织唯一标识符 (OUI)</p></td>
<td><p>3</p></td>
<td><p>0x00、 0x50，0xF2</p></td>
<td><p>供应商 (Microsoft)</p></td>
</tr>
<tr class="even">
<td><p>OUI 类型</p></td>
<td><p>1</p></td>
<td><p>0X11</p></td>
<td><p>OUI 类型 （网络成本）</p></td>
</tr>
<tr class="odd">
<td><p>成本的属性 （必需）</p></td>
<td><p>4</p></td>
<td><p>变量</p></td>
<td><p>DWORD，little endian 字节顺序</p></td>
</tr>
</tbody>
</table>

 

下图显示了成本属性字段的格式：

![格式成本属性字段](images/fig1-mb-format-cost-attr-field.jpg)

下表显示可能成本级别位 （一个是必需的）：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>“属性”</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01</p></td>
<td><p>Unrestricted</p></td>
<td><p>不增加成本适用于此连接上传输数据。</p></td>
</tr>
<tr class="even">
<td><p>0x02</p></td>
<td><p>固定</p></td>
<td><p>数据传输按流量计费的和计算根据数据限制。 成本没有区别适用此限制内。</p></td>
</tr>
<tr class="odd">
<td><p>0x04</p></td>
<td><p>变量</p></td>
<td><p>在此链接上的所有使用应用增量费用。</p></td>
</tr>
</tbody>
</table>

 

下表显示了可能成本标志位：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>名称</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0x01 00 00</p></td>
<td><p>超过数据限制</p></td>
<td><p>使用率已超过数据限制和不同的网络成本或条件适用。</p></td>
</tr>
<tr class="even">
<td><p>0x02 00 00</p></td>
<td><p>拥塞</p></td>
<td><p>遇到网络运营商或大量负载和请求应为较少活动，在可能的情况。</p></td>
</tr>
<tr class="odd">
<td><p>0x04 00 00</p></td>
<td><p>Roaming</p></td>
<td><p>连接提供商的家庭网络或关联公司之外漫游。</p></td>
</tr>
<tr class="even">
<td><p>0x08 00 00</p></td>
<td><p>接近数据限制</p></td>
<td><p>使用情况即将达到数据上限中;不同的网络成本或条件可能很快就适用。</p></td>
</tr>
</tbody>
</table>

 

下表显示了某些示例成本属性值：

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
<td><p>不受限制的连接;标准 WLAN 由固定宽带提供支持。</p></td>
</tr>
<tr class="even">
<td><p>便携式热点默认</p></td>
<td><p>0x00 00 00 02</p></td>
<td><p>按流量计费的网络;限制未知或尚未达到;匹配 Windows 移动宽带连接的默认值。</p></td>
</tr>
<tr class="odd">
<td><p>通过限制 / 限制</p></td>
<td><p>0x00 01 00 01</p></td>
<td><p>用户已超过数据限制;速度会减少，但没有更多的使用情况限制适用。</p></td>
</tr>
<tr class="even">
<td><p>通过限制 / 费用</p></td>
<td><p>0x00 01 00 04</p></td>
<td><p>用户已超过数据限制;其他使用情况会产生增量费用。</p></td>
</tr>
<tr class="odd">
<td><p>便携式热点漫游</p></td>
<td><p>0x00 04 00 04</p></td>
<td><p>漫游连接;由于网络状态应用增量费用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idaddnetworkcostsupporttoyourdevicespanspan-idaddnetworkcostsupporttoyourdevicespanspan-idaddnetworkcostsupporttoyourdevicespanadd-network-cost-support-to-your-device"></a><span id="Add_network_cost_support_to_your_device"></span><span id="add_network_cost_support_to_your_device"></span><span id="ADD_NETWORK_COST_SUPPORT_TO_YOUR_DEVICE"></span>将网络成本支持添加到你的设备


1.  添加到你的设备 WLAN 信标和探测响应，固定为 IE**便携式热点默认**成本示例属性值与表中所示的值。 验证 Windows 8、 Windows 8.1 或 Windows 10 计算机将自动连接到此网络选择**减少网络利用率**为此网络的选项。

2.  漫游时，将为默认值保有**便携式热点 / 漫游**示例表中列出的值成本属性值。

3.  （可选） 使用您的合作伙伴运营商，以确定其他值可能是适当的如下所示的情况下：

    -   时 （LTE、 HSPA + 等），某些承载上不受限制

    -   定义的通道检测到超出限制状态。

    -   当超过数据限制运算符定义的行为。

4.  （可选） 如果你的设备可用作第二个跃点网络的 Wi-fi，检查此网络的连接并中继到您自己的 SSID 其值 （或其不存在） 上的 IE。 如果不存在，则使用**默认 WLAN**示例表中列出的值成本属性值。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[通信通道](communication-channels.md)

 

 






