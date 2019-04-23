---
title: OID_WDI_SET_ADAPTER_CONFIGURATION
description: OID_WDI_SET_ADAPTER_CONFIGURATION 配置适配器。 它是一个可选属性，并且只能在创建的任何端口之前发送。
ms.assetid: d1c37943-4755-4b9e-ab9c-9378aeca9c03
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADAPTER_CONFIGURATION 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: e7fe2a1cb746e720cffdafbd51c09c5f766ec5d9
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902347"
---
# <a name="oidwdisetadapterconfiguration"></a>OID\_WDI\_SET\_ADAPTER\_CONFIGURATION


OID\_WDI\_设置\_适配器\_配置配置的适配器。 它是一个可选属性，并且只能在创建的任何端口之前发送。

| 范围   | 设置与任务序列化 | 正常执行时间 （秒） |
|---------|--------------------------|---------------------------------|
| 适配器 | 是                      | 1                               |

 

## <a name="set-property-parameters"></a>设置属性参数


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
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926257" data-raw-source="[&lt;strong&gt;WDI_TLV_CONFIGURED_MAC_ADDRESS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926257)"><strong>WDI_TLV_CONFIGURED_MAC_ADDRESS</strong></a></td>
<td></td>
<td>X</td>
<td>MAC 地址。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898075" data-raw-source="[&lt;strong&gt;WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898075)"><strong>WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD</strong></a></td>
<td></td>
<td>X</td>
<td>无法访问检测阈值。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897879" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897879)"><strong>WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY</strong></a></td>
<td></td>
<td>X</td>
<td>固件用于运行后 Wi-Fi Direct 转重置通道选择策略是停止/重新启动。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926145" data-raw-source="[&lt;strong&gt;WDI_TLV_BAND_ID_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926145)"><strong>WDI_TLV_BAND_ID_LIST</strong></a></td>
<td></td>
<td>X</td>
<td>带区 Id 的列表。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897841" data-raw-source="[&lt;strong&gt;WDI_TLV_LINK_QUALITY_BAR_MAP&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897841)"><strong>WDI_TLV_LINK_QUALITY_BAR_MAP</strong></a></td>
<td></td>
<td></td>
<td>为 Wi-fi 信号强度图条的信号质量的映射。 此字段应忽略由适配器和它应使用中指定的行为<a href="ndis-status-wdi-indication-link-state-change.md" data-raw-source="[NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE](ndis-status-wdi-indication-link-state-change.md)">NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE</a>进行链接质量通知。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt269108" data-raw-source="[&lt;strong&gt;WDI_TLV_ADAPTER_NLO_SCAN_MODE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt269108)"><strong>WDI_TLV_ADAPTER_NLO_SCAN_MODE</strong></a></td>
<td></td>
<td>X</td>
<td>指示是否应在主动或被动模式下执行 NLO 扫描。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt593243" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593243)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></td>
<td></td>
<td></td>
<td>在 Windows 10 版本 1511，WDI 版本 1.0.10 中添加。
<p>指定是否支持 PLDR。</p></td>
</tr>
</tbody>
</table>

 

## <a name="set-property-results"></a>设置属性结果


没有其他数据。 标头中的数据就足够了。

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
<td>Dot11wdi.h</td>
</tr>
</tbody>
</table>

 

 




