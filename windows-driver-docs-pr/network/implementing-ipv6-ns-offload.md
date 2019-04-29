---
title: 实现 IPv6 NS 卸载
description: 本部分介绍如何实现 IPv6 邻居招标 (NS) 卸载
ms.assetid: 48AACE46-4D39-49ED-90AD-F73E27D0CDBE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 685fecb635c435e52ecd5a3f7adde5d6075fbab8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363065"
---
# <a name="implementing-ipv6-ns-offload"></a>实现 IPv6 NS 卸载


NDIS 协议驱动程序将发送 (NS) 卸载请求作为 IPv6 邻居招标[OID\_PM\_添加\_协议\_卸载](https://msdn.microsoft.com/library/windows/hardware/ff569763)OID 请求。 若要支持这些 NS 卸载请求，微型端口应执行以下操作。

## <a name="indicating-how-many-offload-requests-the-miniport-adapter-supports"></a>指示多少卸载请求微型端口适配器支持


微型端口驱动程序设置**NumNSOffloadIPv6Addresses**的成员[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)结构，以指示多少 NS卸载请求微型端口适配器支持。

**请注意**  尽管其名称**NumNSOffloadIPv6Addresses**成员包含的支持请求，不是数字的地址数。

 

**请注意**  某些 Windows 硬件认证要求，如**Device.Network.LAN.PM.PowMgmtNDIS**并**Device.Network.WLAN.WoWLAN.ImplementWakeOnWLAN**，指定的微型端口适配器必须支持至少 2 个 NS 卸载请求。 (即，以满足这些要求的值**NumNSOffloadIPv6Addresses**必须至少为 2。)有关详细信息，请参阅[Windows 8 硬件认证要求](https://go.microsoft.com/fwlink/p/?linkid=268621)。

 

每个 NS 卸载请求可以包含 1 或 2 个目标地址。

此外，还有两种类型的 NS 消息： 单播和多播。 微型端口驱动程序必须准备好与两种类型的每个目标地址的 NS 消息相匹配。

### <a name="example"></a>示例

如果微型端口驱动程序设置[ **NDIS\_PM\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff566748)隶属**NumNSOffloadIPv6Addresses**然后 NDIS 可能为 3，结构发送最多 3 个[OID\_PM\_添加\_协议\_卸载](https://msdn.microsoft.com/library/windows/hardware/ff569763)类型的请求**NdisPMProtocolOffloadIdIPv6NS**。 每个 OID\_PM\_添加\_协议\_卸载请求中可以有完全 1 或 2 个地址**TargetIPv6Addresses**隶属[ **NDIS\_PM\_协议\_卸载**](https://msdn.microsoft.com/library/windows/hardware/ff566760)结构。 因此，微型端口必须支持 3 x 2 = 6 目标地址。

由于微型端口必须匹配这两个单播和多播的 NS 消息为每个目标地址，微型端口应该能够匹配总共 6 x 2 = 12 NS 消息模式。

## <a name="matching-the-ns-message"></a>NS 消息相匹配


中指定 NS 消息格式[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)部分 4.3，"邻居请求消息格式"。 微型端口应与下表中的字段匹配。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>Ethernet.EtherType</strong></td>
<td align="left"><p>0x86dd (IPv6)</p></td>
<td align="left"><p>调整所需的非以太网的媒体类型。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.Version</strong></td>
<td align="left"><p>6</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.NextHeader</strong></td>
<td align="left"><p>58 (ICMPv6)</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.Destination</strong></td>
<td align="left"><p><strong>OID.TargetIPv6Addresses[x]</strong> or <strong>OID.SolicitedNodeIPv6Address</strong></p></td>
<td align="left"><p>微型端口必须匹配此字段的这两个选项：<strong>OID。TargetIPv6Addresses [x]</strong>和<strong>OID。SolicitedNodeIPv6Address</strong>。</p>
<p>如果此字段为<strong>OID。TargetIPv6Addresses [x]</strong>，NS 消息是单播消息。</p>
<p>如果此字段为<strong>OID。SolicitedNodeIPv6Address</strong>，NS 消息是多路广播的消息。</p>
<p><strong>OID。TargetIPv6Addresses</strong>是一个数组，其中可以包含 1 或 2 个地址。 如果它包含 2 个地址，微型端口必须与匹配这两个值。 如果第二个地址，"0::0"必须忽略它，并且必须创建第二个匹配模式。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.Type</strong></td>
<td align="left"><p>135 (NS)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.Code</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><p><strong>OID.TargetIPv6Addresses[x]</strong></p></td>
<td align="left"><p><strong>OID。TargetIPv6Addresses [x]</strong>是一个数组，其中可以包含 1 或 2 个地址。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.Source</strong></td>
<td align="left"><p><strong>OID.RemoteIPv6Address</strong></p></td>
<td align="left"><p>如果<strong>OID。RemoteIPv6Address</strong>是"0::0"，应忽略此字段。</p></td>
</tr>
</tbody>
</table>

 

## <a name="sending-the-na-message"></a>发送 NA 消息


收到 NS 消息时，设备固件应执行验证步骤中调用[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)部分 7.1 中，"消息验证"，包括验证校验和。 如果传入的 NS 消息通过所有验证，然后 NA 消息必须生成和发送作为回复。 中指定它的格式[RFC 4861](https://go.microsoft.com/fwlink/p/?linkid=268370)部分 4.4，"邻居公告消息格式"。 微型端口应该设置下表中的字段。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">字段</th>
<th align="left">ReplTest1</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>Ethernet.Destination</strong></td>
<td align="left"><strong>Ethernet.Source</strong></td>
<td align="left"><p>NS 帧中复制此值。 调整所需的非以太网的媒体类型。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>Ethernet.Source</strong></td>
<td align="left"><p>微型端口的当前的 MAC 地址</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.HopLimit</strong></td>
<td align="left"><p>255</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.Source</strong></td>
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><p>NS 帧中复制此值。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.Destination</strong></td>
<td align="left"><strong>IPv6.Source</strong></td>
<td align="left"><p>除非从 NS 帧中，复制此值的值<strong>IPv6.Source</strong>已"0::0"。 如果的值<strong>IPv6.Source</strong>已"0::0"设置此字段为"ff02:: 1"。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.Type</strong></td>
<td align="left"><p>136 (NA)</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.Code</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.RouterFlag</strong></td>
<td align="left"><p>0</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.SolicitedFlag</strong></td>
<td align="left"><p>0</p></td>
<td align="left"><p>如果的值<strong>IPv6.Source</strong> NS 在帧是"0::0"，将此字段设置为 1。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.OverrideFlag</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><strong>IPv6.ICMPv6.TargetAddress</strong></td>
<td align="left"><p>NS 帧中复制此值。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.TLLAOption.Type</strong></td>
<td align="left"><p>2 （目标链路层地址）</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><strong>IPv6.ICMPv6.TLLAOption.Length</strong></td>
<td align="left"><p>1</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><strong>IPv6.ICMPv6.TLLAOption.LinkLayerAddress</strong></td>
<td align="left"><strong>OID.MacAddress</strong></td>
<td align="left"></td>
</tr>
</tbody>
</table>

 

 

 





