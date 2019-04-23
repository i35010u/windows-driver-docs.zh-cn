---
title: WDI_TLV_STATION_CAPABILITIES
description: WDI_TLV_STATION_CAPABILITIES 是 TLV 包含工作站的功能。
ms.assetid: 567445F1-EEDC-4302-B709-ED76D044A971
ms.date: 02/08/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_STATION_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 70b35e7549410cf9d7e1cf8dc2cc623865d23b26
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903256"
---
# <a name="wditlvstationcapabilities"></a>WDI\_TLV\_工作站\_功能


WDI\_TLV\_工作站\_功能是 TLV 包含工作站的功能。

## <a name="tlv-type"></a>TLV 类型


0x11

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
<td>UINT32</td>
<td>扫描 SSID 列表的大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>所需的 BSSID 列表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>所需的 SSID 列表大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>隐私例外列表的大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>密钥映射表的大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>默认表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>WEP 密钥值的最大长度。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>每 STA 默认键表的最大数。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>支持 QoS 标志。 指定设备是否支持 WMM。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否实现主机 FIPS 模式。
<p>如果该字段与任何其他设置的位设置为 DOT11_EXTSTA_ATTRIBUTES_SAFEMODE_OID_SUPPORTED，驱动程序实现操作的 802.11 安全模式。</p>
<p>如果该字段设置为 DOT11_EXTSTA_ATTRIBUTES_SAFEMODE_CERTIFIED，NIC 已收到来自美国国家标准和技术协会 (NIST) 联邦信息处理标准 (FIPS) 发布 140-2 下的验证证书加密模块的安全要求。 在此模式下，硬件负责确保符合 FIPS 标准。</p>
<p>如果该字段设置为零 (0)，FIPS 模式未实现的 nic。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定是否 802.11w MFP 功能支持。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否支持自动节能。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定适配器是否保持工作站 BSS 列表缓存。
<p>有效值为 0 （否） 和 1 (yes)。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定适配器是否可能会尝试为期间工作站首选 BSSID 列表中未指定 bssid 时关联连接。
<p>有效值为 0 （否） 和 1 (yes)。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的最大的网络卸载列表的大小。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定适配器可以跟踪 HESSIDs 与 Ssid 和仅对匹配指定的 SSID + HESSID 这些 APs 连接/漫游相关联。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定适配器是否可以卸载到属于特定 HESSIDs 网络连接。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否支持已断开连接待机状态。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定驱动程序是否支持作为发起方的正常时间度量 (FTM) 协议。
<p>有效值为 0 （不支持） 和 1 （支持）。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>可以查询每个 FTM 请求任务的目标 Sta 最大数目。</td>
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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




