---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO 是包含 Wi-Fi 直接组所有者协商请求信息的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 49693fac97b2c99c2a9b9eb3b014877f250d2277
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818791"
---
# <a name="wdi_tlv_p2p_go_negotiation_request_info"></a>WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 请求 \_ 信息


WDI \_ tlv \_ P2P \_ 中转 \_ 协商 \_ 请求 \_ 信息是一个 TLV，其中包含 Wi-Fi 直接组所有者协商请求信息。

## <a name="tlv-type"></a>TLV 类型


0x6D

## <a name="length"></a>长度


Sum (包含所有 TLVs 的大小的) 字节。

## <a name="values"></a>值


| 类型                                                                                                         | 允许多个 TLV 实例 | 可选 | 说明                                                                                                                         |
|--------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 请求 \_ 参数**](wdi-tlv-p2p-go-negotiation-request-parameters.md) |                                |          | Wi-Fi 直接组所有者协商请求参数。                                                                        |
| [**WDI \_ TLV \_ P2P \_ 信道 \_ 号**](wdi-tlv-p2p-channel-number.md)                                         |                                | X        | 远程设备的侦听通道。 只要指定了此协议，就必须在此通道上发送 "中转协商请求" 帧。 |

 

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

 

 




