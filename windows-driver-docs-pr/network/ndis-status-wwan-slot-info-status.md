---
title: NDIS_STATUS_WWAN_SLOT_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SLOT_INFO 通知来通知 MB 服务完成了以前的 OID_WWAN_SLOT_INFO 查询请求。
ms.assetid: FA1E16E4-56A3-4401-875F-D75DD01FE75D
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_SLOT_INFO 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ce116993d1b9a7ad29896672edac33c87edfcb2d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844640"
---
# <a name="ndis_status_wwan_slot_info"></a>\_WWAN\_槽\_信息的 NDIS\_状态


微型端口驱动程序使用**NDIS\_状态\_WWAN\_槽\_信息**通知来通知 MB 服务完成以前的[OID\_WWAN\_槽\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)查询请求。

小型端口驱动程序可以将**NDIS\_状态\_WWAN\_槽\_信息**通知发送到插槽/卡状态发生更改时的未经请求的事件。

此通知使用[**NDIS\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>Windows 10 版本1703</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_槽\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)

[**NDIS\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

 

 




