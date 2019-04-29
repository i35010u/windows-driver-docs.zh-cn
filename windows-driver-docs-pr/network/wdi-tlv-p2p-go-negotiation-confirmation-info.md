---
title: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO 是包含 Wi-Fi Direct 转协商确认信息 TLV。
ms.assetid: 1CC470FF-9301-4DF9-BE52-5FB1DCBF5415
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 14acd2c2a81ab3abb1b01f9f0cd287b3b4e269cf
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362485"
---
# <a name="wditlvp2pgonegotiationconfirmationinfo"></a>WDI\_TLV\_P2P\_转\_协商\_确认\_信息


WDI\_TLV\_P2P\_转\_协商\_确认\_信息是包含 Wi-Fi Direct 转协商确认信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x88

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                                   | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_转\_协商\_确认\_参数**](wdi-tlv-p2p-go-negotiation-confirmation-parameters.md) |                                |          | Wi-Fi Direct 转协商确认参数中。                                                                                |
| [**WDI\_TLV\_P2P\_GROUP\_ID**](wdi-tlv-p2p-group-id.md)                                                               |                                | X        | Wi-Fi Direct 组 id。                                                                                                              |
| [**WDI\_TLV\_P2P\_CHANNEL\_NUMBER**](wdi-tlv-p2p-channel-number.md)                                                   |                                | X        | 远程设备侦听通道。 只要指定此，必须在此通道上发送 GO 协商确认帧。 |

 

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

 

 




