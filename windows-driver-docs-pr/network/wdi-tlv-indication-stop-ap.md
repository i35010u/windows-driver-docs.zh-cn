---
title: WDI_TLV_INDICATION_STOP_AP
description: WDI_TLV_INDICATION_STOP_AP 是一种 TLV，其中包含停止 AP 指示的原因。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: aa499dd172400062e9673a972860132fb65809a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786029"
---
# <a name="wdi_tlv_indication_stop_ap"></a>WDI \_ TLV \_ 指示 \_ 停止 \_ AP


WDI \_ TLV \_ 指示 \_ 停止 \_ ap 是一个 TLV，其中包含停止 AP 指示的原因。

## <a name="tlv-type"></a>TLV 类型


0xE6

## <a name="length"></a>长度


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 描述                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------------------|
| UINT32 | 停止 AP 原因。 有关可能的原因值，请参阅 [**WDI \_ 停止 \_ AP \_ 原因**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_stop_ap_reason) 。 |

 

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

## <a name="see-also"></a>请参阅


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 停止 \_ AP](./ndis-status-wdi-indication-stop-ap.md)

 

