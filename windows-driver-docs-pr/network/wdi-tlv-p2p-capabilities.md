---
title: WDI_TLV_P2P_CAPABILITIES
description: WDI_TLV_P2P_CAPABILITIES 是包含 Wi-Fi Direct 功能 TLV。
ms.assetid: 3BE13A87-ECA2-4204-87F1-2BE393F33D4C
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7673589acdb9a97e4aef4d6a072645bef62e6af8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548072"
---
# <a name="wditlvp2pcapabilities"></a>WDI\_TLV\_P2P\_功能


WDI\_TLV\_P2P\_功能是包含 Wi-Fi Direct 功能 TLV。

## <a name="tlv-type"></a>TLV 类型


0x17

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT8</td>
<td>指定并发组所有者计数。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定并发客户端计数。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定支持的 WPS 版本。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否支持服务发现。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Wi-Fi Direct 服务名称发现支持。 指定是否在给定的服务名称哈希列表，适配器可以探测服务哈希值并指示响应到达。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Wi-Fi Direct 发现服务信息的支持。 指定是否在给定的服务名称哈希列表，该适配器可以执行探测和 ANQP 查询以获取完整的服务的信息。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定服务名称播发字节 （要在信标和探测响应中发送） 支持最大的数目。 这可以播发的服务的数量设置是硬性限制。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定受支持的最大适配器可以响应使用天然气协议的服务信息播发字节数。 这是仅设备支持响应服务播发查询时才有效。 此值是固件优化，以便在固件不会唤醒要对每个查询做出响应的主机。 如果固件有一个限制，因为在操作系统中没有回退，操作系统不限制的服务广告的数量。 如果固件不能处理 ANQP 查询响应，它应传递请求和操作系统能够处理它。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Wi-Fi Direct 设备和服务的后台发现。 指定是否该适配器可以定期查询 Wi-Fi Direct 设备和服务名称因此任何新设备显示在 5 分钟内成为可见。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否支持客户端的可发现性。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定是否支持基础结构管理。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>辅助适配器类型列表的最大大小。</td>
</tr>
<tr class="odd">
<td>UINT8[6]</td>
<td>网络字节顺序中的设备地址。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>发现筛选器列表的大小。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>转到客户端表的大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>最大大小，以字节为单位的供应商特定扩展可以添加到 WFD 管理帧的导致浏览器。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定适配器是否支持 OID_WDI_P2P_LISTEN_STATE_PASSIVE_AVAILABILITY。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定适配器是否支持转到操作频道的指示更新。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>在 Windows 10 版本 1511，WDI 版本 1.0.10 中添加。
<p>指定适配器是否支持操作系统上使用 5 GHz 频段 GO。</p>
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td><p>UINT8</p></td>
<td><p>在 Windows 10，版本 1607，WDI 版本 1.0.21 中添加。</p>
指定适配器，在提供一系列 ASP2 服务名称情况下，是否可以探测服务哈希值并指示响应到达。 有效值为 0 （不支持） 和 1 （支持）。</td>
</tr>
<tr class="odd">
<td><p>UINT8</p></td>
<td><p>在 Windows 10，版本 1607，WDI 版本 1.0.21 中添加。</p>
指定的适配器，在给定的一组服务名称实例，是否可以执行探测和 ANQP 查询以获取完整的服务信息。 有效值为 0 （不支持） 和 1 （支持）。</td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




