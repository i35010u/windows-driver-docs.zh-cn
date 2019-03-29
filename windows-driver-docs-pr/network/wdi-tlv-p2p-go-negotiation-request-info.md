---
title: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO 是 TLV 包含 Wi-Fi Direct 组所有者协商请求信息。
ms.assetid: 4F505DF1-8D02-4421-956F-B7E1AF99D367
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_REQUEST_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dc90926dfe3f8664e9de868746233d7010e6df3e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575875"
---
# <a name="wditlvp2pgonegotiationrequestinfo"></a>WDI\_TLV\_P2P\_GO\_NEGOTIATION\_REQUEST\_INFO


WDI\_TLV\_P2P\_转\_协商\_请求\_信息是包含 Wi-Fi Direct 组所有者协商请求信息 TLV。

## <a name="tlv-type"></a>TLV 类型


0x6D

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                         | 允许多个 TLV 实例 | 可选 | 描述                                                                                                                         |
|--------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_GO\_NEGOTIATION\_REQUEST\_PARAMETERS**](wdi-tlv-p2p-go-negotiation-request-parameters.md) |                                |          | Wi-Fi Direct 组所有者协商请求参数。                                                                        |
| [**WDI\_TLV\_P2P\_CHANNEL\_NUMBER**](wdi-tlv-p2p-channel-number.md)                                         |                                | X        | 远程设备侦听通道。 每当指定此选项，必须在此通道上发送 GO 协商请求帧。 |

 

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

 

 




