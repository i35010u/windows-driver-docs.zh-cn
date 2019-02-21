---
title: OID_WDI_GET_ADAPTER_CAPABILITIES
description: OID_WDI_GET_ADAPTER_CAPABILITIES 是一个只读属性，在初始化期间发出从适配器到主机，并请求适配器的功能。
ms.assetid: e79deb29-bc0b-472e-b549-86bf71fe66ff
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_GET_ADAPTER_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: e07449f00f60059f7f87ed18d7abe6da846e8c2b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534621"
---
# <a name="oidwdigetadaptercapabilities"></a>OID\_WDI\_获取\_适配器\_功能


OID\_WDI\_获取\_适配器\_功能是一个只读属性，在初始化期间发出从适配器到主机，并请求适配器的功能。

| 范围   | 设置与任务序列化 | 正常执行时间 （秒） |
|---------|--------------------------|---------------------------------|
| 适配器 | 不支持 set 语句        | 1                               |

 

## <a name="get-property-parameters"></a>获取属性参数


任何其他参数。 标头中的数据就足够了。
## <a name="get-property-results"></a>获取属性的结果


如果适配器支持 Wi-Fi Direct，同时[ **WDI\_TLV\_AP\_特性**](https://msdn.microsoft.com/library/windows/hardware/dn926129)并[ **WDI\_TLV\_P2P\_特性**](https://msdn.microsoft.com/library/windows/hardware/dn897863)必须指定。

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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926255" data-raw-source="[&lt;strong&gt;WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926255)"><strong>WDI_TLV_COMMUNICATION_CONFIGURATION_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>主机适配器通信协议配置属性。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897835" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_ATTRIBUTES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897835)"><strong>WDI_TLV_INTERFACE_ATTRIBUTES</strong></a></td>
<td></td>
<td></td>
<td>接口特性。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898066" data-raw-source="[&lt;strong&gt;WDI_TLV_STATION_ATTRIBUTES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898066)"><strong>WDI_TLV_STATION_ATTRIBUTES</strong></a></td>
<td></td>
<td></td>
<td>工作站属性。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926129" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_ATTRIBUTES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926129)"><strong>WDI_TLV_AP_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>访问点属性。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898078" data-raw-source="[&lt;strong&gt;WDI_TLV_VIRTUALIZATION_ATTRIBUTES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898078)"><strong>WDI_TLV_VIRTUALIZATION_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>虚拟化的属性。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897863" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ATTRIBUTES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897863)"><strong>WDI_TLV_P2P_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>Wi-Fi Direct 属性。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926277" data-raw-source="[&lt;strong&gt;WDI_TLV_DATAPATH_ATTRIBUTES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926277)"><strong>WDI_TLV_DATAPATH_ATTRIBUTES</strong></a></td>
<td></td>
<td>X</td>
<td>数据路径属性。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926146" data-raw-source="[&lt;strong&gt;WDI_TLV_BAND_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926146)"><strong>WDI_TLV_BAND_INFO</strong></a></td>
<td>X</td>
<td>X</td>
<td>带区信息。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898023" data-raw-source="[&lt;strong&gt;WDI_TLV_PHY_INFO&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898023)"><strong>WDI_TLV_PHY_INFO</strong></a></td>
<td>X</td>
<td>X</td>
<td>PHY 信息。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898032" data-raw-source="[&lt;strong&gt;WDI_TLV_PM_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898032)"><strong>WDI_TLV_PM_CAPABILITIES</strong></a></td>
<td></td>
<td>X</td>
<td>电源管理功能。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926268" data-raw-source="[&lt;strong&gt;WDI_TLV_COUNTRY_REGION_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926268)"><strong>WDI_TLV_COUNTRY_REGION_LIST</strong></a></td>
<td></td>
<td>X</td>
<td>国家或地区代码。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898046" data-raw-source="[&lt;strong&gt;WDI_TLV_RECEIVE_COALESCING_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898046)"><strong>WDI_TLV_RECEIVE_COALESCING_CAPABILITIES</strong></a></td>
<td></td>
<td>X</td>
<td>硬件辅助接收筛选器功能。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898069" data-raw-source="[&lt;strong&gt;WDI_TLV_TCP_OFFLOAD_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898069)"><strong>WDI_TLV_TCP_OFFLOAD_CAPABILITIES</strong></a></td>
<td></td>
<td>X</td>
<td>TCP/IP 卸载功能。</td>
</tr>
<tr class="even">
<td><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769918" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769918)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p>在 Windows 10，版本 1607，WDI 版本 1.0.21 中添加。</p>
<p>将传递到 NDIS WDI 查询时的 Guid 的列表<a href="https://msdn.microsoft.com/library/windows/hardware/ff569641" data-raw-source="[OID_GEN_SUPPORTED_GUIDS](https://msdn.microsoft.com/library/windows/hardware/ff569641)">OID_GEN_SUPPORTED_GUIDS</a>。</p></td>
</tr>
<tr class="odd">
<td><p><a href="wdi-tlv-os-power-management-features.md" data-raw-source="[&lt;strong&gt;WDI_TLV_OS_POWER_MANAGEMENT_FEATURES&lt;/strong&gt;](wdi-tlv-os-power-management-features.md)"><strong>WDI_TLV_OS_POWER_MANAGEMENT_FEATURES</strong></a></p></td>
<td></td>
<td></td>
<td><p>在 Windows 10，版本 1803，WDI 版本 1.1.6 中添加。</p>
<p>用于启用高级的操作系统电源管理功能。</p>
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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




