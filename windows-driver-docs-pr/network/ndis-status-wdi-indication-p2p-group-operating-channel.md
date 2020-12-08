---
title: NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL 指示给定的 Wi-Fi 直接端口正在操作的操作通道。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_GROUP_OPERATING_CHANNEL 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1cfcf89ea404fa14ab55049abc308ded0f1c9426
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837119"
---
# <a name="ndis_status_wdi_indication_p2p_group_operating_channel"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 组 \_ 操作 \_ 通道


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 组 \_ 操作 \_ 通道指示给定 Wi-Fi 定向端口正在操作的操作通道。

对于 Wi-Fi 的直接客户端端口，必须在 "连接完成") 之前的 "连接 (中指出此情况。

对于 Wi-Fi 的直接前往端口，必须在 oid 完成) 之前，在 [oid \_ WDI \_ 任务 \_ 启动 \_ AP](oid-wdi-task-start-ap.md) (期间指示这一点。

## <a name="payload-data"></a>负载数据


| 类型                                                                                         | 允许多个 TLV 实例 | 可选 | 说明                                                        |
|----------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 号**](./wdi-tlv-p2p-channel-number.md)                    |                                |          | 给定 Wi-Fi 直接端口正在其上运行的操作通道。 |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Dot11wdi</td>
</tr>
</tbody>
</table>

 

