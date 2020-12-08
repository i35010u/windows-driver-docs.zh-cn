---
title: WDI_TLV_STATION_CAPABILITIES
description: WDI_TLV_STATION_CAPABILITIES 是包含工作站功能的 TLV。
ms.date: 02/08/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_STATION_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 4b4bb5c15e1a21c9fb665084a1b0a6aa23c3f61a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821959"
---
# <a name="wdi_tlv_station_capabilities"></a>WDI \_ TLV \_ 工作站 \_ 功能


WDI \_ tlv \_ 工作站 \_ 功能是包含工作站功能的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x11

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
<td>UINT32</td>
<td>扫描 SSID 列表大小。</td>
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
<td>隐私例外列表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>键映射表大小。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>默认的键表大小。</td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>WEP 密钥值的最大长度。</td>
</tr>
<tr class="even">
<td>UINT32</td>
<td>每个 STA 默认键表的最大数目。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>支持的 QoS 标志。 指定设备是否支持 WMM。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否实现主机 FIPS 模式。
<p>如果该字段设置为 DOT11_EXTSTA_ATTRIBUTES_SAFEMODE_OID_SUPPORTED 没有设置其他位，则驱动程序将实现802.11 安全模式的操作。</p>
<p>如果该字段设置为 "DOT11_EXTSTA_ATTRIBUTES_SAFEMODE_CERTIFIED"，则 NIC 接收到 (美国联邦信息处理标准) 联邦信息处理标准的验证证书， (FIPS) 发布140-2，即加密模块的安全要求。 在此模式下，硬件负责确保符合 FIPS 标准。</p>
<p>如果字段设置为零 (0) ，则 NIC 不会实现 FIPS 模式。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定是否支持 802.11 w MFP 功能。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否支持自动节能。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定适配器是否维护工作站 BSS 列表缓存。
<p>有效值为 0 () ，1 (是) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定在工作站连接期间，适配器是否可能尝试关联到未在首选 BSSID 列表中指定的 BSSID。
<p>有效值为 0 () ，1 (是) 。</p></td>
</tr>
<tr class="odd">
<td>UINT32</td>
<td>支持的最大网络卸载列表大小。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定适配器是否可以跟踪与 Ssid 关联的 HESSIDs，并仅连接/漫游到与指定的 SSID + HESSID 匹配的那些 Ap。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定适配器是否可以卸载到属于特定 HESSIDs 的网络的连接。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指定是否支持断开连接备用。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>指定驱动程序是否支持 (INTERNAL.H) 协议作为发起方的精细时间度量。
<p>有效值为 0 (不支持) 和 1 (支持) 。</p></td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>每个 INTERNAL.H 请求任务可以查询的目标 Sta 的最大数目。</td>
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

 

 




