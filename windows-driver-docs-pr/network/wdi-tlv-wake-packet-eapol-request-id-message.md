---
title: WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE
description: WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE 是一种 TLV，其中包含 EAPOL 请求 ID 消息的 LAN 唤醒模式 ID。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_WAKE_PACKET_EAPOL_REQUEST_ID_MESSAGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 152682ab768342cf25694dd01aa2af957c39b772
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821923"
---
# <a name="wdi_tlv_wake_packet_eapol_request_id_message"></a>WDI \_ TLV \_ 唤醒 \_ 数据包 \_ EAPOL \_ 请求 \_ ID \_ 消息


WDI \_ tlv \_ 唤醒 \_ 数据包 \_ EAPOL \_ 请求 \_ id \_ 消息是一个 TLV，其中包含 EAPOL 请求 id 消息的 LAN 唤醒模式 ID。

## <a name="tlv-type"></a>TLV 类型


0x5F

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                           |
|--------|---------------------------------------|
| UINT32 | 指定 LAN 唤醒模式 ID。 |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




