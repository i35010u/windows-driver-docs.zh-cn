---
title: WDI_TLV_P2P_CAPABILITIES
description: WDI_TLV_P2P_CAPABILITIES 是包含 Wi-Fi 直接功能的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 33656d48e4eefbcba580e48f361a5f3952ee9796
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823759"
---
# <a name="wdi_tlv_p2p_capabilities"></a>WDI \_ TLV \_ P2P \_ 功能


WDI \_ tlv \_ P2P \_ 功能是包含 Wi-Fi 直接功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x17

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
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
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Wi-Fi 直接服务名称发现支持。 指定在给定服务名称哈希列表时，适配器是否可以探测服务哈希，并在响应到达时指示响应。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>Wi-Fi 直接服务信息发现支持。 指定在给定服务名称哈希列表时，适配器是否可以执行探测和 ANQP 查询以获取完整的服务信息。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>指定 (在信标和探测响应) 中发送的最大受支持的服务名称播发字节数。 这会对可以播发的服务数量设置硬限制。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>指定适配器可使用加油站协议响应的最大服务信息播发字节数。 这仅适用于设备支持响应服务播发查询的情况。 此值用于固件优化，因此，固件不会唤醒主机以响应每个查询。 如果固件因为在操作系统中有回退而受到限制，则操作系统不会限制服务播发的数目。 如果固件无法处理 ANQP 查询响应，则它应传递请求，并且操作系统会对其进行处理。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>Wi-Fi 直接设备和服务的后台发现。 指定适配器是否可以定期查询 Wi-Fi 直接设备和服务名称，以便在5分钟内显示任何新设备。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否支持客户端发现。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定是否支持基础结构管理。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>辅助适配器类型列表的最大大小。</td>
</tr>
<tr class="odd">
<td>UINT8 [6]</td>
<td>以网络字节顺序排列的设备地址。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>发现筛选器列表大小。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>"离开客户端" 表的大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>可添加到 WFD 管理帧的供应商特定扩展的最大大小（以字节为单位）。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定适配器是否支持 OID_WDI_P2P_LISTEN_STATE_PASSIVE_AVAILABILITY。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定适配器是否支持指示开始操作通道的更新)  (s。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>已在 Windows 10 版本1511、WDI 版本1.0.10 中添加。
<p>指定适配器是否支持5GHz 带区上的操作。</p>
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td><p>UINT8</p></td>
<td><p>已在 Windows 10 版本1607、WDI 版本1.0.21 中添加。</p>
指定在向 ASP2 服务名称实例列表提供时，适配器是否可以探测服务哈希，并在响应到达时指示响应。 有效值为 0 (不支持) 和 1 (支持) 。</td>
</tr>
<tr class="odd">
<td><p>UINT8</p></td>
<td><p>已在 Windows 10 版本1607、WDI 版本1.0.21 中添加。</p>
指定在给定一组服务名称实例的情况下，适配器是否可以执行探测和 ANQP 查询以获取完整的服务信息。 有效值为 0 (不支持) 和 1 (支持) 。</td>
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




