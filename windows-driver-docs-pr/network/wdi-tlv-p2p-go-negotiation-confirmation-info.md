---
title: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO 是一种 TLV，其中包含 Wi-Fi 的直接中转协商确认信息。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_CONFIRMATION_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f687ff69fe6730be1a546aae0409b08aa0efb2b2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818795"
---
# <a name="wdi_tlv_p2p_go_negotiation_confirmation_info"></a>WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 确认 \_ 信息


WDI \_ tlv \_ \_ 中转 \_ 协商确认 \_ 信息 \_ 是一个 Tlv，其中包含 Wi-Fi 的直接中转协商确认信息。

## <a name="tlv-type"></a>TLV 类型


0x88

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                                   | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                             |
|------------------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 确认 \_ 参数**](wdi-tlv-p2p-go-negotiation-confirmation-parameters.md) |                                |          | Wi-Fi Direct 中转协商确认参数。                                                                                |
| [**WDI \_ TLV \_ P2P \_ 组 \_ ID**](wdi-tlv-p2p-group-id.md)                                                               |                                | X        | Wi-Fi 的直接组 ID。                                                                                                              |
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 号**](wdi-tlv-p2p-channel-number.md)                                                   |                                | X        | 远程设备的侦听通道。 只要指定了此，就必须在此通道上发送中转协商确认帧。 |

 

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

 

 




