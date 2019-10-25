---
title: 实现 IPv6 NS 卸载
description: 本部分介绍如何实现 IPv6 邻居请求（NS）卸载
ms.assetid: 48AACE46-4D39-49ED-90AD-F73E27D0CDBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d31487cbad6874e54437ed5070d8fe103c66d488
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843638"
---
# <a name="implementing-ipv6-ns-offload"></a>实现 IPv6 NS 卸载


NDIS 协议驱动程序以 OID\_PM 的形式发送 IPv6 邻居请求（NS）卸载请求[\_添加\_协议\_卸载](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)OID 请求。 若要支持这些 NS 卸载请求，微型端口应执行以下操作。

## <a name="indicating-how-many-offload-requests-the-miniport-adapter-supports"></a>指示微型端口适配器支持多少卸载请求


微型端口驱动程序将[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构的**NumNSOffloadIPv6Addresses**成员设置为指示微型端口适配器支持的 NS 卸载请求数。

**请注意**  尽管名称相同，但**NumNSOffloadIPv6Addresses**成员包含受支持的请求数，而不是地址的数目。

 

**请注意**，  一些 Windows 硬件认证要求，如**PowMgmtNDIS**和**WoWLAN。 ImplementWakeOnWLAN**，请指定微型端口适配器必须至少支持2个 NS。卸载请求。 （也就是说，若要满足这些要求， **NumNSOffloadIPv6Addresses**的值必须至少为2。）有关详细信息，请参阅[Windows 8 硬件认证要求](https://go.microsoft.com/fwlink/p/?linkid=268621)。

 

每个 NS 卸载请求可包含1个或2个目标地址。

此外，有2种类型的 NS 消息：单播和多播。 小型端口驱动程序必须准备好匹配每个目标地址的 NS 消息类型。

### <a name="example"></a>示例

如果微型端口驱动程序将**NumNSOffloadIPv6Addresses**结构的[**NDIS\_PM\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)成员设置为3，则 ndis 最多可以向3个[\_\_PM 发送\_](https://docs.microsoft.com/windows-hardware/drivers/network/oid-pm-add-protocol-offload)键入**NdisPMProtocolOffloadIdIPv6NS**。 每个 OID\_PM\_添加\_协议\_卸载请求在[**NDIS\_PM\_协议\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_protocol_offload)结构的**TargetIPv6Addresses**成员中可能正好有1或2个地址。 因此，小型端口必须支持 3 x 2 = 6 目标地址。

由于微型端口必须匹配每个目标地址的单播和多播 NS 消息，因此，微型端口应能匹配总共 6 x 2 = 12 个 NS 消息模式。

## <a name="matching-the-ns-message"></a>与 NS 消息匹配


NS 消息格式在[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)第4.3 节 "邻居请求消息格式" 中指定。 小型端口应与下表中的字段匹配。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">匹配值</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>EtherType</strong></td>
<td align="left"><p>0x86dd （IPv6）</p></td>
<td align="left"><p>根据非以太网介质类型的需要进行调整。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6. 版本</strong></td>
<td align="left"><p>6</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>NextHeader</strong></td>
<td align="left"><p>58（ICMPv6）</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6。目标</strong></td>
<td align="left"><p><strong>OID。TargetIPv6Addresses [x]</strong>或<strong>OID。SolicitedNodeIPv6Address</strong></p></td>
<td align="left"><p>小型端口必须与此字段的两个选项匹配： <strong>OID。TargetIPv6Addresses [x]</strong>和<strong>OID。SolicitedNodeIPv6Address</strong>。</p>
<p>如果此字段为 OID，则为<strong>。TargetIPv6Addresses [x]</strong>，NS 消息是单播消息。</p>
<p>如果此字段为 OID，则为<strong>。SolicitedNodeIPv6Address</strong>，NS 消息是一条多播消息。</p>
<p><strong>OID。TargetIPv6Addresses</strong>是一个可包含1个或2个地址的数组。 如果它包含2个地址，则它必须同时匹配这两个地址。 如果第二个地址为 "0::0"，则必须将其忽略，并且不能创建另一个匹配模式。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6。类型</strong></td>
<td align="left"><p>135（NS）</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. 代码</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><p><strong>OID.TargetIPv6Addresses [x]</strong></p></td>
<td align="left"><p><strong>OID。TargetIPv6Addresses [x]</strong>是可以包含1个或2个地址的数组。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6。源</strong></td>
<td align="left"><p><strong>OID.RemoteIPv6Address</strong></p></td>
<td align="left"><p>如果为，则为<strong>。RemoteIPv6Address</strong>是 "0::0"，应忽略此字段。</p></td>
</tr>
</tbody>
</table>

 

## <a name="sending-the-na-message"></a>发送 NA 消息


接收到 NS 消息后，设备固件应执行[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)第7.1 节 "消息验证" 中调用的验证步骤，包括验证校验和。 如果传入 NS 消息通过了所有验证，则必须生成 NA 消息并将其作为答复发送。 其格式在[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)第4.4 节 "邻居广告消息格式" 中指定。 小型端口应设置下表中的字段。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">Value</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>以太网。目标</strong></td>
<td align="left"><strong>以太网。源</strong></td>
<td align="left"><p>从 NS 帧中复制此值。 根据非以太网介质类型的需要进行调整。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>以太网。源</strong></td>
<td align="left"><p>微型端口的当前 MAC 地址</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6。源</strong></td>
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><p>从 NS 帧中复制此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6。目标</strong></td>
<td align="left"><strong>IPv6。源</strong></td>
<td align="left"><p>从 NS 帧复制此值，除非<strong>IPv6</strong>的值是 "0::0"。 如果<strong>IPv6</strong>的值为 "0::0"将此字段设置为 "FF02：： 1"。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6。类型</strong></td>
<td align="left"><p>136（NA）</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6. 代码</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>RouterFlag</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>SolicitedFlag</strong></td>
<td align="left"><p>0</p></td>
<td align="left"><p>如果 NS 帧中的 " <strong>IPv6</strong> " 的值为 "0::0"，则将此字段设置为1。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>OverrideFlag</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><strong>TargetAddress</strong></td>
<td align="left"><p>从 NS 帧中复制此值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>TLLAOption。类型</strong></td>
<td align="left"><p>2（目标链路层地址）</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>TLLAOption. 长度</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>TLLAOption. LinkLayerAddress</strong></td>
<td align="left"><strong>OID.MacAddress</strong></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





