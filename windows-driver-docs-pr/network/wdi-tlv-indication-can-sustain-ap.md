---
title: WDI_TLV_INDICATION_CAN_SUSTAIN_AP
description: WDI_TLV_INDICATION_CAN_SUSTAIN_AP 是一个 TLV，其中包含可承受 AP 指示的原因。
ms.assetid: 9C7B8E8D-BAF4-4DC7-A020-5B0DEC7CC2FB
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_CAN_SUSTAIN_AP 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6dc472ea7b8df822a9f45090f8382a8ff00f0325
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841747"
---
# <a name="wdi_tlv_indication_can_sustain_ap"></a>WDI\_TLV\_指示\_可以\_维持\_AP


WDI\_TLV\_指示\_可以\_维持\_AP 是一个 TLV，其中包含可承受 AP 指示的原因。

## <a name="tlv-type"></a>TLV 类型


0xE7

## <a name="length"></a>长度


UINT32 的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                                        |
|--------|------------------------------------------------------------------------------------------------------------------------------------|
| UINT32 | 可以承受 AP 原因。 有关可能的原因值，请参阅[**WDI\_可以\_维持\_AP\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_can_sustain_ap_reason)。 |

 

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
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS\_状态\_WDI\_指示\_可\_维持\_AP](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-can-sustain-ap)

 

 




