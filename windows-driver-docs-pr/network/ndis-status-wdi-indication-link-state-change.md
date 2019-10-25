---
title: NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 指示以下任何情况
ms.assetid: 5a8fbe41-d063-4d34-beb8-92ceeb1d97a2
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a4a3416109e63b64fbc9c5fc65d9d35d4382deed
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844427"
---
# <a name="ndis_status_wdi_indication_link_state_change"></a>NDIS\_状态\_WDI\_指示\_链接\_状态\_更改


小型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_链接\_状态\_更改为指示以下任何情况：

-   链接速度发生变化。
-   链接质量的变化超出了阈值。 如果 "连接质量提示" 设置为 "\_\_WDI"，则阈值为1，\_低\_延迟（在[**WDI\_连接\_quality\_提示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_connection_quality_hint)中定义）。 否则，阈值为5。

| 对象 |
|--------|
| 端口   |

 

此指示中的此信息由主机用于跟踪有关当前链接的元数据，并且可能传播给用户。

在工作站和 P2P 客户端情况下，对等 MAC 地址设置为连接的网络的 BSSID。 在 AP/P2P 走箱中，对等 MAC 地址设置为指定的已连接设备的 MAC 地址。

## <a name="payload-data"></a>负载数据


| 在任务栏的搜索框中键入                                                                                           | 允许多个 TLV 实例 | 可选 | 描述                       |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI\_TLV\_LINK\_状态\_更改\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-link-state-change-parameters) |                                |          | 链接状态更改参数。 |

 

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
<td><p>Windows 10</p></td>
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

 

 




