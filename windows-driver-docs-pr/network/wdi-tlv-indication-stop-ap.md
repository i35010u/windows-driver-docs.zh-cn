---
title: WDI_TLV_INDICATION_STOP_AP
description: WDI_TLV_INDICATION_STOP_AP 是一个 TLV，其中包含停止 AP 指示的原因。
ms.assetid: 49FA6AF6-68BE-437B-9715-5090F52F0109
ms.date: 07/18/2017
keywords:
- WDI_TLV_INDICATION_STOP_AP 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fc19dfffedc925b07fd8cf53dbdfcb7bdc308935
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841745"
---
# <a name="wdi_tlv_indication_stop_ap"></a>WDI\_TLV\_指示\_停止\_AP


WDI\_TLV\_指示\_停止\_AP 是包含停止 AP 指示原因的 TLV。

## <a name="tlv-type"></a>TLV 类型


0xE6

## <a name="length"></a>长度


UINT32 的大小（以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入   | 描述                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------------------|
| UINT32 | 停止 AP 原因。 有关可能的原因值，请参阅[**WDI\_停止\_AP\_原因**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_stop_ap_reason)。 |

 

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


[NDIS\_状态\_WDI\_指示\_停止\_AP](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wdi-indication-stop-ap)

 

 




