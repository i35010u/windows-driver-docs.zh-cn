---
title: WDI_TLV_P2P_INVITATION_RESPONSE_INFO
description: WDI_TLV_P2P_INVITATION_RESPONSE_INFO 是包含 Wi-Fi 直接邀请响应信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INVITATION_RESPONSE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b215949498f8a7d8dcd2f39e5fca4c8c0d751bd3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818233"
---
# <a name="wdi_tlv_p2p_invitation_response_info"></a>WDI \_ TLV \_ P2P \_ 邀请 \_ 响应 \_ 信息


WDI \_ tlv \_ P2P \_ 邀请 \_ 响应 \_ 信息是一个 Tlv，其中包含 Wi-Fi 直接邀请回复信息。

## <a name="tlv-type"></a>TLV 类型


0x7E

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                  | 允许多个 TLV 实例 | 可选 | 说明                                      |
|-------------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 邀请 \_ 响应 \_ 参数**](wdi-tlv-p2p-invitation-response-parameters.md) |                                |          | Wi-Fi 直接邀请响应参数。 |
| [**WDI \_ TLV \_ P2P \_ 组 \_ BSSID**](wdi-tlv-p2p-group-bssid.md)                                        |                                | X        | 本地 Wi-Fi Direct 中转的组 BSSID。       |
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 号**](wdi-tlv-p2p-channel-number.md)                                  |                                | X        | Wi-Fi 直接走的操作通道。       |

 

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

 

 




