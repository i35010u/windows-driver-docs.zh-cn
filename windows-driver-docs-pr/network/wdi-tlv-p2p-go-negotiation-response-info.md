---
title: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_INFO
description: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_INFO 是 TLV 包含 Wi-Fi Direct 组所有者协商响应信息。
ms.assetid: A0BB2CF6-4168-4973-92D0-EFF9F596F1BE
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ff66fdf272a0c2a480dcd5594f458feeaa6978fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374546"
---
# <a name="wditlvp2pgonegotiationresponseinfo"></a>WDI\_TLV\_P2P\_转\_协商\_响应\_信息


WDI\_TLV\_P2P\_转\_协商\_响应\_信息是 TLV 包含 Wi-Fi Direct 组所有者协商响应信息。

## <a name="tlv-type"></a>TLV 类型


0x6F

## <a name="length"></a>长度


所有的大小 （以字节为单位） 总和包含 TLVs。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                                                                           | 允许多个 TLV 实例 | 可选 | 描述                                                             |
|----------------------------------------------------------------------------------------------------------------|--------------------------------|----------|-------------------------------------------------------------------------|
| [**WDI\_TLV\_P2P\_GO\_NEGOTIATION\_RESPONSE\_PARAMETERS**](wdi-tlv-p2p-go-negotiation-response-parameters.md) |                                |          | 指定 Wi-Fi Direct 组所有者协商响应参数。 |
| [**WDI\_TLV\_P2P\_GROUP\_ID**](wdi-tlv-p2p-group-id.md)                                                       |                                | X        | 指定本地 Wi-Fi Direct 转组 ID。                       |

 

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

 

 




