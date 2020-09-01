---
title: NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 通知来通知 MB 服务完成了上一个 OID_WWAN_DEVICE_SLOT_MAPPING_INFO 查询或设置请求。
ms.assetid: 7825C20E-FB56-420D-B516-1ADA0C7C382E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 13cd3e086b4763c445a4dc25e443cc497105a6b8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212852"
---
# <a name="ndis_status_wwan_device_slot_mapping_info"></a>NDIS \_ 状态 \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息


微型端口驱动程序使用 **NDIS \_ 状态 \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息** 通知来通知 MB 服务完成了上一个 [OID \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息](./oid-wwan-device-slot-mappings.md) 查询或设置请求。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info) 结构。

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


[OID \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息](./oid-wwan-device-slot-mappings.md)

[**NDIS \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

 

