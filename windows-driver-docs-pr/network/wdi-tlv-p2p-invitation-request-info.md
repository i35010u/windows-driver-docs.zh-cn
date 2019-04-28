---
title: WDI_TLV_P2P_INVITATION_REQUEST_INFO
description: WDI_TLV_P2P_INVITATION_REQUEST_INFO 是 TLV 包含 Wi-Fi Direct 邀请请求信息。
ms.assetid: 055B0F6D-2B68-495D-8253-2D213D699383
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INVITATION_REQUEST_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dbd853552a9a8d46c798b735829ed50357058944
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347287"
---
# <a name="wditlvp2pinvitationrequestinfo"></a>WDI\_TLV\_P2P\_邀请\_请求\_信息


WDI\_TLV\_P2P\_邀请\_请求\_信息是包含 Wi-Fi Direct 邀请请求信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x7B

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                | 允许多个 TLV 实例 | 可选 | 描述                                     |
|-----------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------|
| [**WDI\_TLV\_P2P\_INVITATION\_REQUEST\_PARAMETERS**](wdi-tlv-p2p-invitation-request-parameters.md) |                                |          | Wi-Fi Direct 邀请请求的参数。 |
| [**WDI\_TLV\_P2P\_GROUP\_BSSID**](wdi-tlv-p2p-group-bssid.md)                                      |                                | X        | BSSID 组。                                |
| [**WDI\_TLV\_P2P\_CHANNEL\_NUMBER**](wdi-tlv-p2p-channel-number.md)                                |                                | X        | Wi-Fi Direct 转操作通道。      |
| [**WDI\_TLV\_P2P\_GROUP\_ID**](wdi-tlv-p2p-group-id.md)                                            |                                |          | Wi-Fi Direct 转的目标组 ID。        |

 

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

 

 




