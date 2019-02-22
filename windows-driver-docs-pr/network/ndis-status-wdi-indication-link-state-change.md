---
title: NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 指示以下情况下的任何
ms.assetid: 5a8fbe41-d063-4d34-beb8-92ceeb1d97a2
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_LINK_STATE_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2d97774df236ea57dcf280905378584c6922253f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544562"
---
# <a name="ndisstatuswdiindicationlinkstatechange"></a>NDIS\_状态\_WDI\_指示\_链接\_状态\_更改


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_链接\_状态\_更改以指示任何以下情况：

-   更改链接速度。
-   链接质量更改者超过阈值的值。 阈值为 1，如果连接质量提示设置为 WDI\_连接\_质量\_低\_延迟 (在中定义[ **WDI\_连接\_质量\_提示**](https://msdn.microsoft.com/library/windows/hardware/dn897807))。 否则，阈值是 5。

| 对象 |
|--------|
| 端口   |

 

主机使用来自此指示此信息来跟踪有关的当前链接的元数据，它可能会传播到用户。

在工作站和 P2P 客户端的情况下，对等的 MAC 地址设置为 bssid 时的连接的网络。 亚太/P2P 转的情况下，在对等的 MAC 地址设置为给定连接的设备的 MAC 地址。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                           | 允许多个 TLV 实例 | 可选 | 描述                       |
|------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------|
| [**WDI\_TLV\_链接\_状态\_更改\_参数**](https://msdn.microsoft.com/library/windows/hardware/dn897842) |                                |          | 链接状态更改参数。 |

 

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

 

 




