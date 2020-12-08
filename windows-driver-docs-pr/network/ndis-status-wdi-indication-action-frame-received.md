---
title: NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED
description: 微型端口驱动程序使用 NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED 指示已收到操作帧。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WDI_INDICATION_ACTION_FRAME_RECEIVED 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 916ddf96a160a54e1671edd29f40d358d85dfae3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837152"
---
# <a name="ndis_status_wdi_indication_action_frame_received"></a>\_ \_ 已收到 NDIS 状态 WDI \_ 指示 \_ 操作 \_ 帧 \_


微型端口驱动程序 \_ 使用 \_ 已接收的 NDIS 状态 WDI \_ 指示 \_ 操作帧，指示已 \_ \_ 收到操作帧。

| 对象 |
|--------|
| 端口   |

 

## <a name="payload-data"></a>负载数据


| 类型                                                                               | 允许多个 TLV 实例 | 可选 | 说明                                               |
|------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------|
| [**WDI \_ TLV \_ BSSID**](./wdi-tlv-bssid.md)                                      |                                |          | 源的 BSSID。                                  |
| [**WDI \_ TLV \_ BSS \_ 条目 \_ 通道 \_ 信息**](./wdi-tlv-bss-entry-channel-info.md) |                                |          | BSS 条目的逻辑通道号和带区 ID。 |
| [**WDI \_ TLV \_ 操作 \_ 框架 \_ 正文**](./wdi-tlv-action-frame-body.md)            |                                |          | 传入操作框架正文。                           |

 

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

## <a name="see-also"></a>请参阅


[OID \_ WDI \_ 设置 \_ 播发 \_ 信息](oid-wdi-set-advertisement-information.md)

 

