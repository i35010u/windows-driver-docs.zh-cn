---
title: NDIS_STATUS_WWAN_SLOT_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SLOT_INFO 通知来通知 MB 服务完成了上一个 OID_WWAN_SLOT_INFO 查询请求。
ms.assetid: FA1E16E4-56A3-4401-875F-D75DD01FE75D
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_SLOT_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7ce3cf2a2fe20f4c90fc60f46c5a29a55136c591
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217276"
---
# <a name="ndis_status_wwan_slot_info"></a>NDIS \_ 状态 \_ WWAN \_ 槽 \_ 信息


微型端口驱动程序使用 **NDIS \_ 状态 \_ wwan \_ 槽 \_ 信息** 通知来通知 MB 服务完成了上一个 [OID \_ WWAN \_ 槽 \_ 信息](./oid-wwan-slot-info-status.md) 查询请求。

当槽/插卡状态发生变化时，微型端口驱动程序可以将 **NDIS \_ 状态 \_ WWAN \_ 槽 \_ 信息** 通知发送为未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info) 结构。

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


[OID \_ WWAN \_ 槽 \_ 信息](./oid-wwan-slot-info-status.md)

[**NDIS \_ WWAN \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

 

