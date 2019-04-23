---
title: OID_WDI_TASK_START_AP
description: OID_WDI_TASK_START_AP 请求 IHV 组件配置的端口指定端口上启动 Wi-Fi Direct 组所有者。
ms.assetid: 647b039b-eb9a-43e7-9027-15a55df62c79
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 OID_WDI_TASK_START_AP 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 1631e42945f5e4e73177003dbcbe45b50cc764fe
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903361"
---
# <a name="oidwditaskstartap"></a>OID\_WDI\_TASK\_START\_AP


OID\_WDI\_任务\_启动\_AP 请求 IHV 组件配置的端口指定端口上启动 Wi-Fi Direct 组所有者。

| Object | 中止支持                                     | 默认优先级 （主机驱动程序策略） | 正常执行时间 （秒） |
|--------|---------------------------------------------------|---------------------------------------|---------------------------------|
| 端口   | 是。 中止后面必须跟 dot11 重置。 | 4                                     | 1                               |

 

在初始化期间，驱动程序将转到设置中的 5 GHz 外功能[ **WDI\_TLV\_P2P\_功能**](https://msdn.microsoft.com/library/windows/hardware/dn897865)以指示它是否可以开始访问5 GHz 带区上的点。

如果设置 5 GHz 外支持上的 GO，适配器应上播发操作通道中，启动 AP，如果失败，它应重 AP 外通道列表参数中指定的列表。 操作系统将提供有关将此应用程序是否通过设置提供 internet 连接的驱动程序的提示**DOT11\_WFD\_组\_功能\_跨\_连接\_支持**中的标志[ **WDI\_TLV\_P2P\_组\_所有者\_功能**](https://msdn.microsoft.com/library/windows/hardware/dn897954).

如果**MustUseSpecifiedChannel**中[ **WDI\_TLV\_启动\_AP\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn898065) AP 可能的指定返回以下错误之一，如果无法在指定的带区上启动 AP / 频道。

|                                                                 |                                                                                                         |
|-----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------|
| **NDIS\_状态\_DOT11\_AP\_通道\_当前\_不\_可用** | 无法指定频道上立即启动 AP。 稍后重试上指定的频道。 |
| **NDIS\_状态\_DOT11\_AP\_外\_当前\_不\_可用**    | 无法立即启动上指定的带区上的 AP。 稍后重试上指定的带区。        |
| **NDIS\_状态\_DOT11\_AP\_通道\_不\_允许**              | 无法启动 AP 上指定频道由于需要遵从法规。                           |
| **NDIS\_STATUS\_DOT11\_AP\_BAND\_NOT\_ALLOWED**                 | 无法启动 AP 上指定带区上，由于需要遵从法规。                              |

 

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
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898062" data-raw-source="[&lt;strong&gt;WDI_TLV_SSID&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898062)"><strong>WDI_TLV_SSID</strong></a></td>
<td></td>
<td></td>
<td>将由 AP SSID。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898065" data-raw-source="[&lt;strong&gt;WDI_TLV_START_AP_PARAMETERS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898065)"><strong>WDI_TLV_START_AP_PARAMETERS</strong></a></td>
<td></td>
<td></td>
<td>此任务的其他参数。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn926141" data-raw-source="[&lt;strong&gt;WDI_TLV_AUTH_ALGO_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn926141)"><strong>WDI_TLV_AUTH_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>可以使用该连接的身份验证算法的列表。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897847" data-raw-source="[&lt;strong&gt;WDI_TLV_MULTICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897847)"><strong>WDI_TLV_MULTICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>可以使用该连接的多路广播的密码算法的列表。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn898074" data-raw-source="[&lt;strong&gt;WDI_TLV_UNICAST_CIPHER_ALGO_LIST&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn898074)"><strong>WDI_TLV_UNICAST_CIPHER_ALGO_LIST</strong></a></td>
<td></td>
<td></td>
<td>可以使用该连接的多路广播的密码算法的列表。</td>
</tr>
<tr class="even">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/dn897869" data-raw-source="[&lt;strong&gt;WDI_TLV_P2P_CHANNEL_NUMBER&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/dn897869)"><strong>WDI_TLV_P2P_CHANNEL_NUMBER</strong></a></td>
<td></td>
<td>X</td>
<td>如果指定，此项定义组形成中确定的操作通道。 这仅 Wi-Fi Direct 转运行模式时指定。</td>
</tr>
<tr class="odd">
<td><a href="https://msdn.microsoft.com/library/windows/hardware/mt593242" data-raw-source="[&lt;strong&gt;WDI_TLV_AP_BAND_CHANNEL&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/mt593242)"><strong>WDI_TLV_AP_BAND_CHANNEL</strong></a></td>
<td>X</td>
<td>X</td>
<td>在 Windows 10 版本 1511，WDI 版本 1.0.10 中添加。
<p>可选的带区和通道上启动的访问点的列表。 如果 MustUseSpecifiedChannels 设置为 1，AP 只能启动此列表中。 如果未设置，此列表应提供建议的固件，可以选择的通道，它可能会选取另一个通道，如果不能在任何指定的通道上启动 AP。</p></td>
</tr>
</tbody>
</table>

 

## <a name="task-completion-indication"></a>指示任务完成


[NDIS\_状态\_WDI\_指示\_启动\_AP\_完成](ndis-status-wdi-indication-start-ap-complete.md)

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

 

 




