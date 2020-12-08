---
title: NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES
description: 小型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES 指示开始使用的首选操作通道、首选侦听通道（如果要求进入侦听状态）和所有支持的通道（在任意时间点）。 此指示将在适配器初始化后发送一次，并在每次由于诸如漫游或连接或断开连接访问点的事件而发生更改时发送。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_P2P_OPERATING_CHANNEL_ATTRIBUTES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b2d5a821eaf4901848fe54508c04dbcc963f8520
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789695"
---
# <a name="ndis_status_wdi_indication_p2p_operating_channel_attributes"></a>NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 操作 \_ 通道 \_ 属性


微型端口驱动程序使用 NDIS \_ 状态 \_ WDI \_ 指示 \_ P2P \_ 操作 \_ 通道 \_ 属性来指示首选的操作通道，如要开始使用，首选侦听通道（如果要求进入侦听状态）和所有支持的通道（在任意时间点）。 此指示将在适配器初始化后发送一次，并在每次由于诸如漫游或连接或断开连接访问点的事件而发生更改时发送。

| 对象 |
|--------|
| 端口   |

 

操作通道和通道列表值为 "本地设置"，在 "前往协商/邀请期间不考虑实际的通道协商"。 执行 "执行协商/邀请" 时，驱动程序仍应与通道协商。

如果开启了侦听状态，则会遵守驱动程序报告的侦听通道。 如果主机配置的侦听通道不同于先前通过此指示报告的首选侦听通道，则会触发此指示。

## <a name="payload-data"></a>负载数据


| 类型                                                                                       | 允许多个 TLV 实例 | 可选 | 说明                                              |
|--------------------------------------------------------------------------------------------|--------------------------------|----------|----------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 号**](./wdi-tlv-p2p-channel-number.md)                  |                                |          | Wi-Fi Direct 操作通道特性。            |
| [**WDI \_ TLV \_ P2P \_ 通道 \_ 列表 \_ 属性**](./wdi-tlv-p2p-channel-list-attribute.md) |                                |          | 本地适配器支持的整套通道。 |
| [**WDI \_ TLV \_ P2P \_ 侦听 \_ 通道**](./wdi-tlv-p2p-listen-channel.md)                  |                                |          | Wi-Fi 直接侦听通道特性。               |

 

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

 

