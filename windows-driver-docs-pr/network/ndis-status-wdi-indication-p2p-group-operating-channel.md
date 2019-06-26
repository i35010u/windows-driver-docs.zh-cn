---
title: NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL 指示给定的 Wi-Fi Direct 端口操作所用操作系统的通道。
ms.assetid: 170e5df7-3128-4942-869d-45206022dfaa
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 08ec77366e9ca507cede911b500594b8e9a628dd
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67382658"
---
# <a name="ndisstatuswdiindicationp2pgroupoperatingchannel"></a>NDIS\_状态\_WDI\_指示\_P2P\_组\_操作系统\_通道


微型端口驱动程序使用 NDIS\_状态\_WDI\_指示\_P2P\_组\_操作系统\_通道以指示哪些操作通道给定的 Wi-Fi Direct 端口是操作系统上。

对于 Wi-Fi Direct 客户端端口，此值必须表示期间 （在之前的连接完成） 连接。

对于 Wi-Fi Direct 转端口，此值必须表示期间[OID\_WDI\_任务\_启动\_AP](oid-wdi-task-start-ap.md) （在之前的 OID 完成）。

## <a name="payload-data"></a>有效负载数据


| 在任务栏的搜索框中键入                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                        |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_CHANNEL\_NUMBER**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-number)                    |                                |          | 操作通道给定 Wi-Fi Direct 端口上运行。 |
| [**WDI\_TLV\_P2P\_CHANNEL\_INDICATE\_REASON**](https://docs.microsoft.com/windows-hardware/drivers/network/wdi-tlv-p2p-channel-indicate-reason) |                                |          | 发送所指示的原因。                             |

 

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

 

 




