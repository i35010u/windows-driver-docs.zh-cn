---
title: NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 通知来告知 MB 服务关于完成的上一个 OID_WWAN_DEVICE_SLOT_MAPPING_INFO 查询或设置请求。
ms.assetid: 7825C20E-FB56-420D-B516-1ADA0C7C382E
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_WWAN_DEVICE_SLOT_MAPPING_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 377091b9d384f111021c836f144c86816fffb241
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357263"
---
# <a name="ndisstatuswwandeviceslotmappinginfo"></a>NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息


微型端口驱动程序使用**NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息**通知来通知有关 MB 服务在前一次完成[OID\_WWAN\_设备\_槽\_映射\_信息](https://msdn.microsoft.com/library/windows/hardware/mt799831)查询或设置请求。

微型端口驱动程序不能使用此通知将发送未经请求的事件。

使用此通知[ **NDIS\_WWAN\_设备\_槽\_映射\_信息**](https://msdn.microsoft.com/library/windows/hardware/mt782403)结构。

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


[OID\_WWAN\_DEVICE\_SLOT\_MAPPING\_INFO](https://msdn.microsoft.com/library/windows/hardware/mt799831)

[**NDIS\_WWAN\_DEVICE\_SLOT\_MAPPING\_INFO**](https://msdn.microsoft.com/library/windows/hardware/mt782403)

 

 




