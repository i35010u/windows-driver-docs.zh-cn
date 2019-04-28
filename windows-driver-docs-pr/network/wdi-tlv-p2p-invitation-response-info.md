---
title: WDI_TLV_P2P_INVITATION_RESPONSE_INFO
description: WDI_TLV_P2P_INVITATION_RESPONSE_INFO 是 TLV 包含 Wi-Fi Direct 邀请响应信息。
ms.assetid: DFF1649A-1CBE-4E0B-8EB2-6E10F539C72F
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INVITATION_RESPONSE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c22055bf6c9deedb95d2dd076b8c6a45dad76104
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347230"
---
# <a name="wditlvp2pinvitationresponseinfo"></a>WDI\_TLV\_P2P\_邀请\_响应\_信息


WDI\_TLV\_P2P\_邀请\_响应\_信息是 TLV 包含 Wi-Fi Direct 邀请响应信息。

## <a name="tlv-type"></a>TLV 类型


0x7E

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                  | 允许多个 TLV 实例 | 可选 | 描述                                      |
|-------------------------------------------------------------------------------------------------------|--------------------------------|----------|--------------------------------------------------|
| [**WDI\_TLV\_P2P\_邀请\_响应\_参数**](wdi-tlv-p2p-invitation-response-parameters.md) |                                |          | Wi-Fi Direct 邀请响应参数。 |
| [**WDI\_TLV\_P2P\_GROUP\_BSSID**](wdi-tlv-p2p-group-bssid.md)                                        |                                | X        | 针对本地 Wi-Fi Direct GO 组 BSSID。       |
| [**WDI\_TLV\_P2P\_CHANNEL\_NUMBER**](wdi-tlv-p2p-channel-number.md)                                  |                                | X        | Wi-Fi Direct 转操作通道。       |

 

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
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




