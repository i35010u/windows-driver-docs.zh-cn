---
title: NDIS_STATUS_WWAN_SLOT_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SLOT_INFO 通知来告知 MB 服务关于完成的上一个 OID_WWAN_SLOT_INFO 查询请求。
ms.assetid: FA1E16E4-56A3-4401-875F-D75DD01FE75D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_SLOT_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 0ca1d607ab0e4ca65d5f828b7ac6419f3d16395e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386861"
---
# <a name="ndisstatuswwanslotinfo"></a>NDIS\_状态\_WWAN\_槽\_信息


微型端口驱动程序使用**NDIS\_状态\_WWAN\_槽\_信息**通知来通知 MB 服务有关的上一次完成[OID\_WWAN\_槽\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)查询请求。

微型端口驱动程序可以发送**NDIS\_状态\_WWAN\_槽\_信息**为未经请求事件槽/卡状态发生更改时通知。

使用此通知[ **NDIS\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>Windows 10，版本 1703</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_SLOT\_INFO](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-slot-info-status)

[**NDIS\_WWAN\_SLOT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

 

 




