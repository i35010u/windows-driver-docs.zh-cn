---
title: OID_WDI_GET_ADAPTER_CAPABILITIES
description: OID_WDI_GET_ADAPTER_CAPABILITIES 是一个只读属性，该属性在初始化期间从主机颁发给适配器，并请求适配器的功能。
ms.assetid: e79deb29-bc0b-472e-b549-86bf71fe66ff
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_ADAPTER_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f84f433685c3e635d842ff281f5396a162d7d2ce
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213301"
---
# <a name="oid_wdi_get_adapter_capabilities"></a>OID \_ WDI \_ 获取 \_ 适配器 \_ 功能


OID \_ WDI \_ 获取 \_ 适配器 \_ 功能是一个只读属性，该属性在初始化期间从主机颁发给适配器，并请求适配器的功能。

| 作用域   | 设置序列化任务 | 正常执行时间 (秒)  |
|---------|--------------------------|---------------------------------|
| 适配器 | 不支持的设置        | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


无其他参数。 标头中的数据足够了。
## <a name="get-property-results"></a>获取属性结果


如果适配器支持 Wi-fi Direct，则必须指定 [**WDI \_ tlv \_ AP \_ **](./wdi-tlv-ap-attributes.md) 属性和 [**WDI \_ tlv \_ P2P \_ 属性**](./wdi-tlv-p2p-attributes.md) 。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>TLV</th>
<th>允许多个 TLV 实例</th>
<th>可选</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-communication-configuration-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES&lt;/strong&gt;](./wdi-tlv-communication-configuration-attributes.md)"><strong>WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>主机适配器通信协议配置特性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_ATTRIBUTES&lt;/strong&gt;](./wdi-tlv-interface-attributes.md)"><strong>WDI_TLV_INTERFACE_ATTRIBUTES</strong></a></td>
<td></td>
<td></td>
<td>接口特性。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-station-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_STATION_ATTRIBUTES&lt;/strong&gt;](./wdi-tlv-station-attributes.md)"><strong>WDI_TLV_STATION_ATTRIBUTES</strong></a></td>
<td></td>
<td></td>
<td>工作站属性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_ATTRIBUTES&lt;/strong&gt;](./wdi-tlv-ap-attributes.md)"><strong>WDI_TLV_AP_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>访问点属性。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-virtualization-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_VIRTUALIZATION_ATTRIBUTES&lt;/strong&gt;](./wdi-tlv-virtualization-attributes.md)"><strong>WDI_TLV_VIRTUALIZATION_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>虚拟化属性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ATTRIBUTES&lt;/strong&gt;](./wdi-tlv-p2p-attributes.md)"><strong>WDI_TLV_P2P_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>Wi-fi Direct 特性。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-datapath-attributes" data-raw-source="[&lt;strong&gt;WDI_TLV_DATAPATH_ATTRIBUTES&lt;/strong&gt;](./wdi-tlv-datapath-attributes.md)"><strong>WDI_TLV_DATAPATH_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>数据路径属性。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-band-info" data-raw-source="[&lt;strong&gt;WDI_TLV_BAND_INFO&lt;/strong&gt;](./wdi-tlv-band-info.md)"><strong>WDI_TLV_BAND_INFO</strong></a></td>
<td>X</td>
<td>X</td>
<td>带区信息。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-phy-info" data-raw-source="[&lt;strong&gt;WDI_TLV_PHY_INFO&lt;/strong&gt;](./wdi-tlv-phy-info.md)"><strong>WDI_TLV_PHY_INFO</strong></a></td>
<td>X</td>
<td>X</td>
<td>PHY 信息。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pm-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_PM_CAPABILITIES&lt;/strong&gt;](./wdi-tlv-pm-capabilities.md)"><strong>WDI_TLV_PM_CAPABILITIES</strong></a></td>
<td></td>
<td>X</td>
<td>电源管理功能。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-country-region-list" data-raw-source="[&lt;strong&gt;WDI_TLV_COUNTRY_REGION_LIST&lt;/strong&gt;](./wdi-tlv-country-region-list.md)"><strong>WDI_TLV_COUNTRY_REGION_LIST</strong></a></td>
<td></td>
<td>X</td>
<td>国家或地区代码。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-receive-coalescing-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_RECEIVE_COALESCING_CAPABILITIES&lt;/strong&gt;](./wdi-tlv-receive-coalescing-capabilities.md)"><strong>WDI_TLV_RECEIVE_COALESCING_CAPABILITIES</strong></a></td>
<td></td>
<td>X</td>
<td>硬件辅助接收筛选器功能。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-tcp-offload-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_TCP_OFFLOAD_CAPABILITIES&lt;/strong&gt;](./wdi-tlv-tcp-offload-capabilities.md)"><strong>WDI_TLV_TCP_OFFLOAD_CAPABILITIES</strong></a></td>
<td></td>
<td>X</td>
<td>TCP/IP 卸载功能。</td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](./wdi-tlv-supported-guids.md)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>已在 Windows 10 版本1607、WDI 版本1.0.21 中添加。</p>
<p>查询 WDI 时，传递给 NDIS 的 Guid 列表将用于 <a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-supported-guids" data-raw-source="[OID_GEN_SUPPORTED_GUIDS](./oid-gen-supported-guids.md)">OID_GEN_SUPPORTED_GUIDS</a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wdi-tlv-os-power-management-features.md" data-raw-source="[&lt;strong&gt;WDI_TLV_OS_POWER_MANAGEMENT_FEATURES&lt;/strong&gt;](wdi-tlv-os-power-management-features.md)"><strong>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES</strong></a></p></td>
<td></td>
<td></td>
<td><p>已在 Windows 10 版本1803、WDI 版本1.1.6 中添加。</p>
<p>用于启用高级操作系统电源管理功能。</p>
</td>
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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

