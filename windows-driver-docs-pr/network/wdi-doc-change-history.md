---
title: WDI 文档更改历史记录
description: 本部分列出了 WDI 文档页面的文档更改历史记录
ms.assetid: 29268059-9C33-4768-8F80-195CB28B4663
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: b0457ebe0460f16448c4fa517e449972636fa272
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384342"
---
# <a name="wdi-doc-change-history"></a>WDI 文档更改历史记录

## <a name="windows-10-version-1903"></a>Windows 10 版本 1903

更新到 WDI 版本 1.1.8 的文档。

| 主题 | 描述 |
| --- | --- |
| [WDI_TLV_STATION_CAPABILITIES](wdi-tlv-station-capabilities.md) | 添加了的对驱动程序来指示支持正常计时度量 (FTM)。 |
| [OID_WDI_TASK_REQUEST_FTM](oid-wdi-task-request-ftm.md) | 新添加的任务使 WDI 中以请求，适配器启动 FTM 过程，才能获取往返时间 (RTT) 和位置配置信息 (LCI) 报表从 BSS 目标的 OID。 |
| [WDI_TLV_FTM_REQUEST_TIMEOUT](wdi-tlv-ftm-request-timeout.md) | 新添加的 TLV FTM 请求。 |
| [WDI_TLV_FTM_TARGET_BSS_ENTRY](wdi-tlv-ftm-target-bss-entry.md) | 新添加的 TLV FTM 请求。 |
| [WDI_TLV_REQUEST_LCI_REPORT](wdi-tlv-request-lci-report.md) | 新添加的 TLV FTM 请求。 |
| [NDIS_STATUS_WDI_INDICATION_REQUEST_FTM_COMPLETE](ndis-status-wdi-indication-request-ftm-complete.md) | 新添加的主机发送的任务完成指示为 OID_WDI_TASK_REQUEST_FTM 状态指示。 包含从 BSS 目标 FTM 响应的列表。 |
| [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_FTM_RESPONSE_STATUS](wdi-tlv-ftm-response-status.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_RETRY_AFTER](wdi-tlv-retry-after.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_FTM_NUMBER_OF_MEASUREMENTS](wdi-tlv-ftm-number-of-measurements.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_RTT](wdi-tlv-rtt.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_RTT_ACCURACY](wdi-tlv-rtt-accuracy.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_RTT_VARIANCE](wdi-tlv-rtt-variance.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_LCI_REPORT_STATUS](wdi-tlv-lci-report-status.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_LCI_REPORT_BODY](wdi-tlv-lci-report-body.md) | 新添加的 TLV FTM 响应。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | 指示支持 Multiband 操作 (MBO) 和信号报表卸载驱动程序添加了新的功能。 |
| [**WDI_ASSOC_STATUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status) | 添加**WDI_ASSOC_STATUS_ASSOCIATION_DISALLOWED**状态。 |
| [WPA3 SAE 身份验证](wpa3-sae-authentication.md) | 新 WPA3 SAE （安全身份验证的等于） 身份验证概述。 |
| [WDI_TLV_INTERFACE_CAPABILITIES](wdi-tlv-interface-capabilities.md) | 指示支持 SAE 身份验证的驱动程序添加了新功能。 |
| [**WDI_AUTH_ALGORITHM**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm) | 添加定义**WDI_AUTH_ALGO_WPA3_SAE**。 |
| [NDIS_STATUS_WDI_INDICATION_SAE_AUTH_PARAMS_NEEDED](ndis-status-wdi-indication-sae-auth-params-needed.md) | 新添加的驱动程序发送到请求 SAE 身份验证参数从 WDI 状态指示。 |
| [WDI_TLV_SAE_INDICATION_TYPE](wdi-tlv-sae-indication-type.md) | 新添加的 SAE 身份验证参数请求的 TLV。 |
| [WDI_TLV_SAE_COMMIT_RESPONSE](wdi-tlv-sae-commit-response.md) | 新添加的 SAE 身份验证参数请求的 TLV。 |
| [WDI_TLV_SAE_CONFIRM_RESPONSE](wdi-tlv-sae-confirm-response.md) | 新添加的 SAE 身份验证参数请求的 TLV。 |
| [WDI_TLV_SAE_STATUS](wdi-tlv-sae-status.md) | 新添加的 TLV SAE 身份验证参数请求，以及如何设置 SAE 身份验证参数。 |
| [OID_WDI_SET_SAE_AUTH_PARAMS](oid-wdi-set-sae-auth-params.md) | 新添加的属性包含发送 SAE 提交或确认请求或错误消息指示无法执行与 BSSID SAE 所必需的参数的 OID。 |
| [WDI_TLV_SAE_REQUEST_TYPE](wdi-tlv-sae-request-type.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_COMMIT_REQUEST](wdi-tlv-sae-commit-request.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_FINITE_CYCLIC_GROUP](wdi-tlv-sae-finite-cyclic-group.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_SCALAR](wdi-tlv-sae-scalar.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_ELEMENT](wdi-tlv-sae-element.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_ANTI_CLOGGING_TOKEN](wdi-tlv-sae-anti-clogging-token.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_CONFIRM_REQUEST](wdi-tlv-sae-confirm-request.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_SEND_CONFIRM](wdi-tlv-sae-send-confirm.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [WDI_TLV_SAE_CONFIRM](wdi-tlv-sae-confirm.md) | 新添加的设置 SAE 身份验证参数的 TLV。 |
| [OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME](oid-wdi-task-p2p-send-request-action-frame.md) | 添加了额外的验证 P2P 导致浏览器上传出操作帧。 |
| [OID_WDI_TASK_P2P_SEND_RESPONSE_ACTION_FRAME](oid-wdi-task-p2p-send-response-action-frame.md) | 添加了额外的验证 P2P 导致浏览器上传出操作帧。 || 

## <a name="windows-10-version-1809"></a>Windows 10 版本 1809

更新到 WDI 1.1.7 版本的文档。

| 主题 | 描述 |
| --- | --- |
| [**WDI_PHY_TYPE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_phy_type) | 添加了对 802.11ax PHY。 |
| [**WDI_CONNECTION_QUALITY_HINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_connection_quality_hint) | 更改的名称**WDI_CONNECTION_QUALITY_HIGH_CHANNEL_AVAILABILITY**值设置为**WDI_CONNECTION_QUALITY_HIGH_THROUGHPUT**。 未更改此值的说明。 |
| [NDIS_STATUS_WDI_INDICATION_DEVICE_SERVICE_EVENT](ndis-status-wdi-indication-device-service-event.md) | 添加了的对未经请求的设备服务通知。 |

## <a name="windows-10-version-1803"></a>Windows 10 版本 1803

更新到 WDI 版本 1.1.6 的文档。

| 主题 | 描述 |
| --- | --- |
| [**WDI_TLV_OS_POWER_MANAGEMENT_FEATURES**](wdi-tlv-os-power-management-features.md) | 添加到此 TLV [OID_WDI_GET_ADAPTER_CAPABILITIES](oid-wdi-get-adapter-capabilities.md)以指示哪些操作系统电源管理 (PM) 功能，该驱动程序支持。 |
| [**WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY**](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) | 更新驱动程序现在必须返回 GTK/iGTK 密钥信息，如果已配置，当查询中指定此 TLV [OID_WDI_GET_PM_PROTOCOL_OFFLOAD](oid-wdi-get-pm-protocol-offload.md)。 |
| [NDIS_STATUS_WDI_INDICATION_CIPHER_KEY_UPDATED](ndis-status-wdi-indication-cipher-key-updated.md) | 添加此指示当密钥已更新，而该驱动程序未处于卸载状态时提供通知的 GTK/iGTK 关键更新的驱动程序。 |
| [*MINIPORT_WDI_TX_SUSPECT_FRAME_LIST_ABORT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_suspect_frame_list_abort) | 更新*TxSuspectFrameListAbortHandle*到*TxSuspectFrameListAbort*。 |

## <a name="windows-10-version-1709"></a>Windows 10 版本 1709

更新到 WDI 1.1.5 版本的文档。

| 主题 | 描述 |
| --- | --- |
| [WDI_TLV_TCP_OFFLOAD_CAPABILITIES](wdi-tlv-tcp-offload-capabilities.md) | 添加了新的[ **WDI_TLV_OFFLOAD_SCOPE** ](wdi-tlv-offload-scope.md)参数以指示是否卸载指定应用于应用的 STA 端口仅或所有端口。 |
| [NDIS_STATUS_WDI_INDICATION_SEND_AP_ASSOCIATION_RESPONSE_COMPLETE](ndis-status-wdi-indication-send-ap-association-response-complete.md) | 更改[ **WDI\_TLV\_PHY\_类型\_列表**](wdi-tlv-phy-type-list.md)以使其所需的参数。 |
| [用户启动使用 IHV 跟踪日志记录的反馈](user-initiated-feedback-with-ihv-trace-logging.md) | 添加了一个新的部分介绍如何添加 IHV 用户启动反馈方案上进行日志记录。 |

## <a name="windows10-version-1607"></a>Windows 10，版本 1607


更新为版本 1.0.21 WDI 的文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover" data-raw-source="[OID_WDI_TASK_P2P_DISCOVER](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-p2p-discover)">OID_WDI_TASK_P2P_DISCOVER</a></p></td>
<td align="left"><p>添加了新的任务参数：</p>
<ul>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities" data-raw-source="[OID_WDI_GET_ADAPTER_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-get-adapter-capabilities)">OID_WDI_GET_ADAPTER_CAPABILITIES</a></p></td>
<td align="left"><p>添加了新的 get 属性结果：<a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm)"><strong>WDI_CIPHER_ALGORITHM</strong></a></p></td>
<td align="left"><p>添加的新值：<strong>WDI_CIPHER_ALGO_GCMP</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_phy_type" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_phy_type)"><strong>WDI_PHY_TYPE</strong></a></p></td>
<td align="left"><p>添加的新值：<strong>WDI_PHY_TYPE_DMG</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_p2p_service_discovery_type)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></p></td>
<td align="left"><p>添加了新值：</p>
<ul>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY</strong></li>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION</strong></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-service-information-discovery-entry)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-include-listen-channel)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name)"><strong>WDI_TLV_P2P_INSTANCE_NAME</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name-hash" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME_HASH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-instance-name-hash)"><strong>WDI_TLV_P2P_INSTANCE_NAME_HASH</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type)"><strong>WDI_TLV_P2P_SERVICE_TYPE</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type-hash" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE_HASH&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-service-type-hash)"><strong>WDI_TLV_P2P_SERVICE_TYPE_HASH</strong></a></p>
<p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-supported-guids)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td align="left"><p>新添加的 TLVs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-advertised-services" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-advertised-services)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICES</strong></a></p></td>
<td align="left"><p>添加了包含的 TLV:<a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-asp2-advertised-service-entry)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-interface-capabilities)"><strong>WDI_TLV_INTERFACE_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加一个新值，指定设备是否支持 IP 停靠功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加一个新值，指定是否支持 ASP2 服务名称发现。</p>
<p>添加一个新值，指定是否支持 ASP2 服务发现信息。</p></td>
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
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_DEINIT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_deinit)"><em>MINIPORT_WDI_TX_TARGET_DESC_DEINIT</em></a></p></td>
<td align="left"><p>添加了的 IHV 微型端口不允许在此调用的上下文中进行的任何指示的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_INIT&lt;/em&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dot11wdi/nc-dot11wdi-miniport_wdi_tx_target_desc_init)"><em>MINIPORT_WDI_TX_TARGET_DESC_INIT</em></a></p></td>
<td align="left"><p>添加了的 IHV 微型端口不允许在此调用的上下文中进行的任何指示的说明。</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10-version-1511"></a>Windows 10 版本 1511


更新到 WDI 版本 1.0.10 的文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap" data-raw-source="[OID_WDI_TASK_START_AP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap)">OID_WDI_TASK_START_AP</a></p></td>
<td align="left"><p>添加了新的任务参数：<a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-adapter-configuration" data-raw-source="[OID_WDI_SET_ADAPTER_CONFIGURATION](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-set-adapter-configuration)">OID_WDI_SET_ADAPTER_CONFIGURATION</a></p></td>
<td align="left"><p>添加了新的任务参数：<a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></p></td>
<td align="left"><p>新添加的 TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-capabilities)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加一个新值，指定适配器是否支持操作系统上使用 5 GHz 频段 GO。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-pldr-support)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></p></td>
<td align="left"><p>新添加的 TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></p></td>
<td align="left"><p>添加一个新值，指定是否允许旧 SoftAP 客户端进行连接。</p>
<p>添加一个新值，指定是否在 AP，仅可以在中指定的通道上启动<a href="https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap" data-raw-source="[OID_WDI_TASK_START_AP](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wdi-task-start-ap)">OID_WDI_TASK_START_AP</a>任务的参数<a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel)"> <strong>WDI_TLV_AP_BAND_CHANNEL</strong> </a>.</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10"></a>Windows 10


初始版本。

 

 





