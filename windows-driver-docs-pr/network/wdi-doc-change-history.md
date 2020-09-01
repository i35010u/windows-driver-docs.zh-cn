---
title: WDI 文档更改历史记录
description: 本部分列出 WDI 文档页的文档更改历史记录
ms.assetid: 29268059-9C33-4768-8F80-195CB28B4663
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 28c62742c6e6518501ffbfc0a90bb920dd2cf8a1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216538"
---
# <a name="wdi-doc-change-history"></a>WDI 文档更改历史记录

## <a name="windows-10-version-1903"></a>Windows 10 版本 1903

已更新到 WDI 版本1.1.8 的文档。

| 主题 | 说明 |
| --- | --- |
| [WDI_TLV_STATION_CAPABILITIES](wdi-tlv-station-capabilities.md) | 添加了对驱动程序的支持，以指示支持精细计时度量 (INTERNAL.H) 。 |
| [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md) | 新添加的任务 OID，使 WDI 能够请求适配器启动)  (RTT 获取往返时间和位置配置信息 (来自 BSS 目标的 LCI) 报告。 |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | 新添加的 TLV 用于 INTERNAL.H 请求。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | 新添加的 TLV 用于 INTERNAL.H 请求。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | 新添加的 TLV 用于 INTERNAL.H 请求。 |
| [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md) | 主机发送的新添加的状态指示，作为 OID_WDI_TASK_REQUEST_FTM 的任务完成指示。 包含来自 BSS 目标的 INTERNAL.H 响应列表。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | 新添加的 TLV 用于 INTERNAL.H 响应。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | 为驱动程序添加了新功能，以指示支持 Multiband 操作 (MBO) 和信标报表卸载。 |
| [**WDI_ASSOC_STATUS**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status) | 添加了 **WDI_ASSOC_STATUS_ASSOCIATION_DISALLOWED** 状态。 |
| [WPA3-SAE 身份验证](wpa3-sae-authentication.md) | 全新概述 WPA3-SAE (安全身份验证等于) authentication。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | 增加了驱动程序的新功能，以指示支持 SAE authentication。 |
| [**WDI_AUTH_ALGORITHM**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm) | 添加了 **WDI_AUTH_ALGO_WPA3_SAE**的定义。 |
| [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) | 驱动程序发送的新添加的状态指示，用于从 WDI 请求 SAE authentication 参数。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | 新添加的 TLV 用于 SAE authentication 参数请求。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | 新添加的 TLV 用于 SAE authentication 参数请求。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-confirm-response.md) | 新添加的 TLV 用于 SAE authentication 参数请求。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | 新添加的 TLV 用于 SAE authentication 参数请求和设置 SAE authentication 参数。 |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) | 新添加的属性 OID，其中包含发送 SAE Commit 或 Confirm 请求所需的参数，或指示无法使用 BSSID 执行 SAE 的错误消息。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-confirm-request.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | 新添加的 TLV 用于设置 SAE authentication 参数。 |
| [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md) | 在传出操作帧上增加了对 P2P 的额外验证。 |
| [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md) | 在传出操作帧上增加了对 P2P 的额外验证。 || 

## <a name="windows-10-version-1809"></a>Windows 10 版本 1809

已更新到 WDI 版本1.1.7 的文档。

| 主题 | 说明 |
| --- | --- |
| [**WDI_PHY_TYPE**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type) | 添加了对 802.11 ax PHY 的支持。 |
| [**WDI_CONNECTION_QUALITY_HINT**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint) | 已将 **WDI_CONNECTION_QUALITY_HIGH_CHANNEL_AVAILABILITY** 值的名称更改为 **WDI_CONNECTION_QUALITY_HIGH_THROUGHPUT**。 不会更改此值的说明。 |
| [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md) | 添加了对未经请求的设备服务通知的支持。 |

## <a name="windows-10-version-1803"></a>Windows 10 版本 1803

已更新到 WDI 版本1.1.6 的文档。

| 主题 | 说明 |
| --- | --- |
| [**WDI_TLV_OS_POWER_MANAGEMENT_FEATURES**](wdi-tlv-os-power-management-features.md) | 已将此 TLV 添加到 [OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md) ，以指示驱动程序支持哪些操作系统电源管理 (PM) 功能。 |
| [**WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY**](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) | 更新了此 TLV，以指定在 [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)中查询时，驱动程序现在必须返回 GTK/iGTK 密钥信息（如果已配置）。 |
| [NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md) | 为驱动程序添加了这一指示，以便在更新密钥时提供 GTK/iGTK 密钥更新通知，同时驱动程序未处于卸载状态。 |
| [*MINIPORT_WDI_TX_SUSPECT_FRAME_LIST_ABORT*](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_suspect_frame_list_abort) | 已将 *TxSuspectFrameListAbortHandle* 更新为 *TxSuspectFrameListAbort*。 |

## <a name="windows-10-version-1709"></a>Windows 10 版本 1709

已更新到 WDI 版本1.1.5 的文档。

| 主题 | 说明 |
| --- | --- |
| [WDI_TLV_TCP_OFFLOAD_CAPABILITIES](wdi-tlv-tcp-offload-capabilities.md) | 添加了新的 [**WDI_TLV_OFFLOAD_SCOPE**](wdi-tlv-offload-scope.md) 参数，用于指示指定的或不应用于 STA 端口还是所有端口。 |
| [NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE](ndis-status-wdi-indication-send-ap-association-response-complete.md) | 更改了 [**WDI \_ TLV \_ PHY \_ 类型 \_ 列表**](wdi-tlv-phy-type-list.md) 参数，使其成为必需。 |
| [用户使用 IHV 跟踪日志记录发起的反馈](user-initiated-feedback-with-ihv-trace-logging.md) | 添加了介绍如何将 IHV 日志记录添加到用户启动的反馈方案的新部分。 |

## <a name="windows10-version-1607"></a>Windows 10 版本1607


已更新到 WDI 版本1.0.21 的文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover" data-raw-source="[OID_WDI_TASK_P2P_DISCOVER](./oid-wdi-task-p2p-discover.md)">OID_WDI_TASK_P2P_DISCOVER</a></p></td>
<td align="left"><p>添加了新的任务参数：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](./wdi-tlv-p2p-asp2-service-information-discovery-entry.md)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](./wdi-tlv-p2p-include-listen-channel.md)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities" data-raw-source="[OID_WDI_GET_ADAPTER_CAPABILITIES](./oid-wdi-get-adapter-capabilities.md)">OID_WDI_GET_ADAPTER_CAPABILITIES</a></p></td>
<td align="left"><p>添加了新的 get 属性结果： <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](./wdi-tlv-supported-guids.md)"> <strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm)"><strong>WDI_CIPHER_ALGORITHM</strong></a></p></td>
<td align="left"><p>添加了新值： <strong>WDI_CIPHER_ALGO_GCMP</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_phy_type)"><strong>WDI_PHY_TYPE</strong></a></p></td>
<td align="left"><p>添加了新值： <strong>WDI_PHY_TYPE_DMG</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></p></td>
<td align="left"><p>添加了新值：</p>
<ul>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY</strong></li>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION</strong></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](./wdi-tlv-p2p-asp2-advertised-service-entry.md)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](./wdi-tlv-p2p-asp2-service-information-discovery-entry.md)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](./wdi-tlv-p2p-include-listen-channel.md)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME&lt;/strong&gt;](./wdi-tlv-p2p-instance-name.md)"><strong>WDI_TLV_P2P_INSTANCE_NAME</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name-hash" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME_HASH&lt;/strong&gt;](./wdi-tlv-p2p-instance-name-hash.md)"><strong>WDI_TLV_P2P_INSTANCE_NAME_HASH</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE&lt;/strong&gt;](./wdi-tlv-p2p-service-type.md)"><strong>WDI_TLV_P2P_SERVICE_TYPE</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type-hash" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE_HASH&lt;/strong&gt;](./wdi-tlv-p2p-service-type-hash.md)"><strong>WDI_TLV_P2P_SERVICE_TYPE_HASH</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](./wdi-tlv-supported-guids.md)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td align="left"><p>新添加的 TLVs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-advertised-services" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICES&lt;/strong&gt;](./wdi-tlv-p2p-advertised-services.md)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICES</strong></a></p></td>
<td align="left"><p>添加了包含的 TLV： <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](./wdi-tlv-p2p-asp2-advertised-service-entry.md)"> <strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_CAPABILITIES&lt;/strong&gt;](./wdi-tlv-interface-capabilities.md)"><strong>WDI_TLV_INTERFACE_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加了新值，该值指定设备是否支持 IP 插接功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](./wdi-tlv-p2p-capabilities.md)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加了新值，该值指定是否支持 ASP2 服务名称发现。</p>
<p>添加了新值，该值指定是否支持 ASP2 服务信息发现。</p></td>
</tr>
</tbody>
</table>

 

## <a name="march-2016"></a>2016 年 3 月


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_DEINIT&lt;/em&gt;](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit)"><em>MINIPORT_WDI_TX_TARGET_DESC_DEINIT</em></a></p></td>
<td align="left"><p>已添加，请注意，不允许 IHV 微型端口在此调用的上下文中作出任何指示。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_INIT&lt;/em&gt;](/windows-hardware/drivers/ddi/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init)"><em>MINIPORT_WDI_TX_TARGET_DESC_INIT</em></a></p></td>
<td align="left"><p>已添加，请注意，不允许 IHV 微型端口在此调用的上下文中作出任何指示。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10-version-1511"></a>Windows 10 版本1511


已更新到 WDI 版本1.0.10 的文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap" data-raw-source="[OID_WDI_TASK_START_AP](./oid-wdi-task-start-ap.md)">OID_WDI_TASK_START_AP</a></p></td>
<td align="left"><p>添加了新的任务参数： <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](./wdi-tlv-ap-band-channel.md)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-adapter-configuration" data-raw-source="[OID_WDI_SET_ADAPTER_CONFIGURATION](./oid-wdi-set-adapter-configuration.md)">OID_WDI_SET_ADAPTER_CONFIGURATION</a></p></td>
<td align="left"><p>添加了新的任务参数： <a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](./wdi-tlv-pldr-support.md)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](./wdi-tlv-ap-band-channel.md)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></p></td>
<td align="left"><p>新添加的 TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](./wdi-tlv-p2p-capabilities.md)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加了新值，指定适配器是否支持5GHz 带区上的操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](./wdi-tlv-pldr-support.md)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></p></td>
<td align="left"><p>新添加的 TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](./wdi-tlv-start-ap-parameters.md)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></p></td>
<td align="left"><p>添加了一个新值，该值指定是否允许旧的 SoftAP 客户端连接。</p>
<p>添加了一个新值，该值指定是否只能在<a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](./wdi-tlv-ap-band-channel.md)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a> <a href="/windows-hardware/drivers/network/oid-wdi-task-start-ap" data-raw-source="[OID_WDI_TASK_START_AP](/windows-hardware/drivers/network/oid-wdi-task-start-ap)">OID_WDI_TASK_START_AP</a>任务参数中指定的通道上启动 AP。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10"></a>Windows 10


初始版本。

 

