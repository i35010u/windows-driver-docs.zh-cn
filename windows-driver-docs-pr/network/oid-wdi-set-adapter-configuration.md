---
title: OID_WDI_SET_ADAPTER_CONFIGURATION
description: OID_WDI_SET_ADAPTER_CONFIGURATION 配置适配器。 它是一个可选属性，只能在创建任何端口之前发送。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_SET_ADAPTER_CONFIGURATION 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 660b5ecade7c5b2fbc5115dc7633d3a144001488
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838729"
---
# <a name="oid_wdi_set_adapter_configuration"></a>OID \_ WDI \_ 设置 \_ 适配器 \_ 配置


OID \_ WDI \_ SET \_ 适配器 \_ 配置配置适配器。 它是一个可选属性，只能在创建任何端口之前发送。

| 范围   | 设置序列化任务 | 正常执行时间 (秒)  |
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
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-configured-mac-address" data-raw-source="[&lt;strong&gt;WDI_TLV_CONFIGURED_MAC_ADDRESS&lt;/strong&gt;](./wdi-tlv-configured-mac-address.md)"><strong>WDI_TLV_CONFIGURED_MAC_ADDRESS</strong></a></td>
<td></td>
<td>X</td>
<td>MAC 地址。</td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-unreachable-detection-threshold" data-raw-source="[&lt;strong&gt;WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD&lt;/strong&gt;](./wdi-tlv-unreachable-detection-threshold.md)"><strong>WDI_TLV_UNREACHABLE_DETECTION_THRESHOLD</strong></a></td>
<td></td>
<td>X</td>
<td>无法访问检测阈值。</td>
</tr>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-p2p-go-internal-reset-policy" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY&lt;/strong&gt;](./wdi-tlv-p2p-go-internal-reset-policy.md)"><strong>WDI_TLV_P2P_GO_INTERNAL_RESET_POLICY</strong></a></td>
<td></td>
<td>X</td>
<td>停止/重新启动 Wi-Fi 的直接重置后，固件用于选择操作通道的策略。</td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-band-id-list" data-raw-source="[&lt;strong&gt;WDI_TLV_BAND_ID_LIST&lt;/strong&gt;](./wdi-tlv-band-id-list.md)"><strong>WDI_TLV_BAND_ID_LIST</strong></a></td>
<td></td>
<td>X</td>
<td>带区 Id 列表。</td>
</tr>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-link-quality-bar-map" data-raw-source="[&lt;strong&gt;WDI_TLV_LINK_QUALITY_BAR_MAP&lt;/strong&gt;](./wdi-tlv-link-quality-bar-map.md)"><strong>WDI_TLV_LINK_QUALITY_BAR_MAP</strong></a></td>
<td></td>
<td></td>
<td>将信号质量映射到 Wi-Fi 信号强度条。 此字段应由适配器忽略，并且应使用 <a href="ndis-status-wdi-indication-link-state-change.md" data-raw-source="[NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE](ndis-status-wdi-indication-link-state-change.md)">NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE</a> 中指定的行为来执行链接质量通知。</td>
</tr>
<tr class="even">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-adapter-nlo-scan-mode" data-raw-source="[&lt;strong&gt;WDI_TLV_ADAPTER_NLO_SCAN_MODE&lt;/strong&gt;](./wdi-tlv-adapter-nlo-scan-mode.md)"><strong>WDI_TLV_ADAPTER_NLO_SCAN_MODE</strong></a></td>
<td></td>
<td>X</td>
<td>指示应在主动还是被动模式下执行 NLO 扫描。</td>
</tr>
<tr class="odd">
<td><a href="/windows-hardware/drivers/network/wdi-tlv-pldr-support" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](./wdi-tlv-pldr-support.md)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></td>
<td></td>
<td></td>
<td>已在 Windows 10 版本1511、WDI 版本1.0.10 中添加。
<p>指定是否支持 PLDR。</p></td>
</tr>
</tbody>
</table>

 

## <a name="set-property-results"></a>设置属性结果


无其他数据。 标头中的数据足够了。

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
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

