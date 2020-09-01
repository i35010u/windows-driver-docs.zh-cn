---
title: NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL 指示给定 Wi-fi Direct 端口正在操作的操作通道。
ms.assetid: 170e5df7-3128-4942-869d-45206022dfaa
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5bb7ebeb54b7e2effeb190b318a9d83c8430c886
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89213455"
---
# <a name="ndis_status_wdi_indication_p2p_group_operating_channel"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 组 \_ 操作 \_ 通道


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 组 \_ 操作 \_ 通道来指示给定 wi-fi Direct 端口正在操作哪个操作通道。

对于 Wi-fi Direct 客户端端口，必须在连接 (期间在连接完成) 之前指定此端口。

对于 Wi-fi Direct 中转端口，必须在 oid [ \_ WDI \_ 任务 \_ 启动 \_ AP](oid-wdi-task-start-ap.md) (期间指定此项，然后) 。

## <a name="payload-data"></a>负载数据


| 类型                                                                                         | 允许多个 TLV 实例 | 可选 | 说明                                                        |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 号**](./wdi-tlv-p2p-channel-number.md)                    |                                |          | 给定 Wi-fi Direct 端口正在其上运行的操作通道。 |
| [**WDI \_ TLV \_ P2P \_ 通道 \_ 指示 \_ 原因**](./wdi-tlv-p2p-channel-indicate-reason.md) |                                |          | 发送指示的原因。                             |

 

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

 

