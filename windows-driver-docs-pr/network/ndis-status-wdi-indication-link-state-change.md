---
title: NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 指示以下任何情况
ms.assetid: 5a8fbe41-d063-4d34-beb8-92ceeb1d97a2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 79a857901fccb5c879e8efec23806c19e04dd8b2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207435"
---
# <a name="ndis_status_wdi_indication_link_state_change"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ 链接 \_ 状态 \_ 更改


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ 链接 \_ 状态 \_ 更改来指示以下任何情况：

-   链接速度发生变化。
-   链接质量的变化超出了阈值。 如果 "连接质量提示" 设置为 "WDI \_ 连接质量 \_ \_ 低 \_ 延迟 (在 [**WDI \_ 连接 \_ 质量 \_ 提示**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)) 中定义，则阈值为1。 否则，阈值为5。

| 对象 |
|--------|
| 端口   |

 

此指示中的此信息由主机用于跟踪有关当前链接的元数据，并且可能传播给用户。

在工作站和 P2P 客户端情况下，对等 MAC 地址设置为连接的网络的 BSSID。 在 AP/P2P 走箱中，对等 MAC 地址设置为指定的已连接设备的 MAC 地址。

## <a name="payload-data"></a>负载数据


| 类型                                                                                           | 允许多个 TLV 实例 | 可选 | 说明                       |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI \_ TLV \_ 链接 \_ 状态 \_ 更改 \_ 参数**](./wdi-tlv-link-state-change-parameters.md) |                                |          | 链接状态更改参数。 |

 

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

 

