---
title: OID_WDI_TASK_START_AP
description: OID_WDI_TASK_START_AP 请求 IHV 组件配置一个端口，以便在指定的端口上启动 Wi-fi Direct 组所有者。
ms.assetid: 647b039b-eb9a-43e7-9027-15a55df62c79
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_START_AP 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 29049cb730f2637c7d6cff3f0f3ffe212b3044a5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89205977"
---
# <a name="oid_wdi_task_start_ap"></a>OID \_ WDI \_ 任务 \_ 启动 \_ AP


OID \_ WDI \_ 任务 \_ 启动 \_ AP 请求 IHV 组件配置一个端口，以便在指定的端口上启动 wi-fi Direct 组所有者。

| 对象 | 支持中止                                     | 主机驱动程序策略 (默认优先级)  | 正常执行时间 (秒)  |
|--------|---------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 中止必须后接 dot11 重置。 | 4                                     | 1                               |

 

在初始化期间，驱动程序会在 [**WDI \_ TLV \_ P2P \_ 功能**](./wdi-tlv-p2p-capabilities.md) 中设置 "使用5ghz 波段" 功能，以指示它是否可以在 5 GHz 波段上启动访问点。

如果设置了 5 GHz 波段支持，适配器应在播发的操作通道上启动 AP，如果失败，则应尝试在 "AP 带区通道列表" 参数中指定的列表。 操作系统将向驱动程序提供提示，指出此 AP 是否可以通过在[**WDI \_ TLV \_ P2P \_ 组 \_ 所有者 \_ 功能**](./wdi-tlv-p2p-group-owner-capability.md)中设置**DOT11 \_ WFD \_ 组 \_ 功能 \_ 交叉 \_ 连接 \_ 支持**的标志来提供 internet 连接。

如果在[**WDI \_ TLV \_ 启动 \_ ap \_ 参数**](./wdi-tlv-start-ap-parameters.md)中指定了**MustUseSpecifiedChannel** ，则当 ap 无法在指定的带 () 上启动 ap 时，它可能会返回以下错误之一。

NDIS \_ 状态 \_ DOT11 \_ AP \_ 通道 \_ 目前 \_ 不可 \_ 用 * * * *：目前无法) 指定通道上启动 ap (s。 稍后在指定的通道上重试 () 。

NDIS \_ 状态 \_ DOT11 \_ \_ 当前不可用 ap 波段 \_ * * * * \_ \_ ：目前无法在指定的频带上启动 ap (s) 。 稍后重试指定的 () 。

\_ \_ \_ 不允许使用 NDIS 状态 DOT11 ap \_ 通道 \_ * * * * \_ ：由于法规原因，无法) 指定的通道上启动 ap (。

\_ \_ \_ 不允许使用 NDIS 状态 DOT11 ap \_ 波段 \_ * * * * \_ ：由于法规原因，无法在指定的带区上启动 ap (s) 。


 

## <a name="task-parameters"></a>任务参数


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
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ssid-list" data-raw-source="[&lt;strong&gt;WDI_TLV_SSID&lt;/strong&gt;](./wdi-tlv-ssid-list.md)"><strong>WDI_TLV_SSID</strong></a></td>
<td></td>
<td></td>
<td>AP 要使用的 SSID。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-start-ap-parameters" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](./wdi-tlv-start-ap-parameters.md)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>此任务的其他参数。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-auth-algo-list" data-raw-source="[&lt;strong&gt;WDI_TLV_AUTH_ALGO_LIST&lt;/strong&gt;](./wdi-tlv-auth-algo-list.md)"><strong>WDI_TLV_AUTH_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>连接可使用的身份验证算法的列表。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-multicast-cipher-algo-list" data-raw-source="[&lt;strong&gt;WDI_TLV_MULTICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](./wdi-tlv-multicast-cipher-algo-list.md)"><strong>WDI_TLV_MULTICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>连接可以使用的多播密码算法的列表。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-unicast-cipher-algo-list" data-raw-source="[&lt;strong&gt;WDI_TLV_UNICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](./wdi-tlv-unicast-cipher-algo-list.md)"><strong>WDI_TLV_UNICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>连接可以使用的多播密码算法的列表。</td>
</tr>
<tr class="even">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-number" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CHANNEL_NUMBER&lt;/strong&gt;](./wdi-tlv-p2p-channel-number.md)"><strong>WDI_TLV_P2P_CHANNEL_NUMBER</strong></a></td>
<td></td>
<td>X</td>
<td>如果已指定，则定义组构成中确定的操作通道。 仅当运行模式为 Wi-fi Direct 中转时，才可以指定此项。</td>
</tr>
<tr class="odd">
<td><a href="https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-ap-band-channel" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](./wdi-tlv-ap-band-channel.md)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></td>
<td>X</td>
<td>X</td>
<td>已在 Windows 10 版本1511、WDI 版本1.0.10 中添加。
<p>要在其上启动访问点的带区和通道的可选列表。 如果 MustUseSpecifiedChannels 设置为1，则只能从此列表中启动 AP。 如果未设置此列表，则此列表应是固件可以选取的通道的建议，如果不能在任何指定的通道上启动 AP，则可以选择另一个通道。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>任务完成指示


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 开始 \_ AP \_ 完成](ndis-status-wdi-indication-start-ap-complete.md)

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

 

