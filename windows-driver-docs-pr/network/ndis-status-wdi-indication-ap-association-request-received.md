---
title: NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED 来指示已为操作 Wi-Fi Direct 组所有者中接收的 Wi-fi 关联请求帧。
ms.assetid: c207ada5-39fd-4326-9b62-4844d3bb01af
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_AP_ASSOCIATION_REQUEST_RECEIVED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 15132e04dd58c0c7de3a2329b04dc31240f8ee7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541809"
---
# <a name="ndisstatuswdiindicationapassociationrequestreceived"></a>NDIS\_STATUS\_WDI\_INDICATION\_AP\_ASSOCIATION\_REQUEST\_RECEIVED


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_AP\_关联\_请求\_接收时间以指示已 Wi-fi 关联请求帧接收到的操作 Wi-Fi Direct 组所有者。 主机可能会发出[OID\_WDI\_任务\_发送\_AP\_关联\_响应](oid-wdi-task-send-ap-association-response.md)此请求。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                                     | 允许多个 TLV 实例 | 可选 | 描述                                   |
|----------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------|
| [**WDI\_TLV\_传入\_关联\_请求\_信息**](https://msdn.microsoft.com/library/windows/hardware/dn926315) |                                |          | 传入的请求关联信息。 |

 

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

 

 




