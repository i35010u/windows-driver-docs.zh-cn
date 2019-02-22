---
title: WDI 文档更改历史记录
description: 本部分列出了 WDI 文档页面的文档更改历史记录
ms.assetid: 29268059-9C33-4768-8F80-195CB28B4663
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3ea98288a032e0ae7d40e6bc25065854696ea53
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544910"
---
# <a name="wdi-doc-change-history"></a>WDI 文档更改历史记录

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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925955" data-raw-source="[OID_WDI_TASK_P2P_DISCOVER](https://msdn.microsoft.com/library/windows/hardware/dn925955)">OID_WDI_TASK_P2P_DISCOVER</a></p></td>
<td align="left"><p>添加了新的任务参数：</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/mt769912" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769912)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/mt769913" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769913)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925838" data-raw-source="[OID_WDI_GET_ADAPTER_CAPABILITIES](https://msdn.microsoft.com/library/windows/hardware/dn925838)">OID_WDI_GET_ADAPTER_CAPABILITIES</a></p></td>
<td align="left"><p>添加了新的 get 属性结果：<a href="https://msdn.microsoft.com/library/windows/hardware/mt769918" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769918)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897802" data-raw-source="[&lt;strong&gt;WDI_CIPHER_ALGORITHM&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897802)"><strong>WDI_CIPHER_ALGORITHM</strong></a></p></td>
<td align="left"><p>添加的新值：<strong>WDI_CIPHER_ALGO_GCMP</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn926105" data-raw-source="[&lt;strong&gt;WDI_PHY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926105)"><strong>WDI_PHY_TYPE</strong></a></p></td>
<td align="left"><p>添加的新值：<strong>WDI_PHY_TYPE_DMG</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn926101" data-raw-source="[&lt;strong&gt;WDI_P2P_SERVICE_DISCOVERY_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926101)"><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE</strong></a></p></td>
<td align="left"><p>添加了新值：</p>
<ul>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_NAME_ONLY</strong></li>
<li><strong>WDI_P2P_SERVICE_DISCOVERY_TYPE_ASP2_SERVICE_INFORMATION</strong></li>
</ul></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769911" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769911)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769912" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769912)"><strong>WDI_TLV_P2P_ASP2_SERVICE_INFORMATION_DISCOVERY_ENTRY</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769913" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769913)"><strong>WDI_TLV_P2P_INCLUDE_LISTEN_CHANNEL</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769914" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769914)"><strong>WDI_TLV_P2P_INSTANCE_NAME</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769915" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_INSTANCE_NAME_HASH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769915)"><strong>WDI_TLV_P2P_INSTANCE_NAME_HASH</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769916" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769916)"><strong>WDI_TLV_P2P_SERVICE_TYPE</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769917" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_SERVICE_TYPE_HASH&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769917)"><strong>WDI_TLV_P2P_SERVICE_TYPE_HASH</strong></a></p>
<p><a href="https://msdn.microsoft.com/library/windows/hardware/mt769918" data-raw-source="[&lt;strong&gt;WDI_TLV_SUPPORTED_GUIDS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769918)"><strong>WDI_TLV_SUPPORTED_GUIDS</strong></a></p></td>
<td align="left"><p>新添加的 TLVs。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897860" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ADVERTISED_SERVICES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897860)"><strong>WDI_TLV_P2P_ADVERTISED_SERVICES</strong></a></p></td>
<td align="left"><p>添加了包含的 TLV:<a href="https://msdn.microsoft.com/library/windows/hardware/mt769911" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt769911)"><strong>WDI_TLV_P2P_ASP2_ADVERTISED_SERVICE_ENTRY</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897836" data-raw-source="[&lt;strong&gt;WDI_TLV_INTERFACE_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897836)"><strong>WDI_TLV_INTERFACE_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加一个新值，指定设备是否支持 IP 停靠功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897865" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897865)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt297593" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_DEINIT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt297593)"><em>MINIPORT_WDI_TX_TARGET_DESC_DEINIT</em></a></p></td>
<td align="left"><p>添加了的 IHV 微型端口不允许在此调用的上下文中进行的任何指示的说明。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt297594" data-raw-source="[&lt;em&gt;MINIPORT_WDI_TX_TARGET_DESC_INIT&lt;/em&gt;](https://msdn.microsoft.com/library/windows/hardware/mt297594)"><em>MINIPORT_WDI_TX_TARGET_DESC_INIT</em></a></p></td>
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
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925964" data-raw-source="[OID_WDI_TASK_START_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)">OID_WDI_TASK_START_AP</a></p></td>
<td align="left"><p>添加了新的任务参数：<a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn925853" data-raw-source="[OID_WDI_SET_ADAPTER_CONFIGURATION](https://msdn.microsoft.com/library/windows/hardware/dn925853)">OID_WDI_SET_ADAPTER_CONFIGURATION</a></p></td>
<td align="left"><p>添加了新的任务参数：<a href="https://msdn.microsoft.com/library/windows/hardware/mt593243" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593243)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></p></td>
<td align="left"><p>新添加的 TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn897865" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CAPABILITIES&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897865)"><strong>WDI_TLV_P2P_CAPABILITIES</strong></a></p></td>
<td align="left"><p>添加一个新值，指定适配器是否支持操作系统上使用 5 GHz 频段 GO。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/mt593243" data-raw-source="[&lt;strong&gt;WDI_TLV_PLDR_SUPPORT&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593243)"><strong>WDI_TLV_PLDR_SUPPORT</strong></a></p></td>
<td align="left"><p>新添加的 TLV。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/dn898065" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898065)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></p></td>
<td align="left"><p>添加一个新值，指定是否允许旧 SoftAP 客户端进行连接。</p>
<p>添加一个新值，指定是否在 AP，仅可以在中指定的通道上启动<a href="https://msdn.microsoft.com/library/windows/hardware/dn925964" data-raw-source="[OID_WDI_TASK_START_AP](https://msdn.microsoft.com/library/windows/hardware/dn925964)">OID_WDI_TASK_START_AP</a>任务的参数<a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"> <strong>WDI_TLV_AP_BAND_CHANNEL</strong> </a>.</p></td>
</tr>
</tbody>
</table>

 

## <a name="windows10"></a>Windows 10


初始版本。

 

 





