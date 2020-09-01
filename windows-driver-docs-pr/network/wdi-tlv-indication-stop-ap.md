---
title: WDI_TLV_INDICATION_STOP_AP
description: WDI_TLV_INDICATION_STOP_AP 是一种 TLV，其中包含停止 AP 指示的原因。
ms.assetid: 49FA6AF6-68BE-437B-9715-5090F52F0109
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_INDICATION_STOP_AP 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 560e8388fe5453a4d9a7e6cf121409a52fa9449a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209597"
---
# <a name="wdi_tlv_indication_stop_ap"></a>WDI \_ TLV \_ 指示 \_ 停止 \_ AP


WDI \_ TLV \_ 指示 \_ 停止 \_ ap 是一个 TLV，其中包含停止 AP 指示的原因。

## <a name="tlv-type"></a>TLV 类型


0xE6

## <a name="length"></a>Length


UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值


| 类型   | 说明                                                                                                  |
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[NDIS \_ 状态 \_ WDI \_ 指示 \_ 停止 \_ AP](./ndis-status-wdi-indication-stop-ap.md)

 

