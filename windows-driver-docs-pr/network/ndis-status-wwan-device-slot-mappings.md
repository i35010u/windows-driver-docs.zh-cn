---
title: NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 通知来通知 MB 服务完成了以前的 OID_WWAN_DEVICE_SLOT_MAPPING_INFO 查询或设置请求。
ms.assetid: 7825C20E-FB56-420D-B516-1ADA0C7C382E
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 56a7f02898b1773d20cce535f5232044142befc6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843030"
---
# <a name="ndis_status_wwan_device_slot_mapping_info"></a>NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息


微型端口驱动程序使用**NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息**通知，通知 MB 服务有关上一个[OID\_WWAN\_设备的完成\_\_映射\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-slot-mappings)查询或设置请求的槽。

微型端口驱动程序无法使用此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)结构。

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


[OID\_WWAN\_设备\_槽\_映射\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-device-slot-mappings)

[**NDIS\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

 

 




