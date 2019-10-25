---
title: OID_WWAN_DEVICE_SLOT_MAPPING_INFO
description: OID_WWAN_DEVICE_SLOT_MAPPING_INFO 设置或返回 MB 设备的设备槽映射（即执行器槽映射）。
ms.assetid: 54AF3447-7918-49CE-945A-DC8DC1E78CBF
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SLOT_MAPPING_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bc74598b3b69f9d27d3fe304b4117ea350f98051
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843853"
---
# <a name="oid_wwan_device_slot_mapping_info"></a>OID\_WWAN\_设备\_槽\_映射\_信息


OID\_WWAN\_设备\_槽\_映射\_信息设置或返回 MB 设备的设备槽映射（即执行器槽映射）。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，然后再发送[**ndis\_状态\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)状态通知，其中包含[**NDIS\_WWAN\_设备\_槽\_映射\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)结构，以提供执行器到槽映射的信息。

下图演示了一个查询请求。

![槽映射查询](images/multi-SIM_8_slotMappingQuery.png)

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，然后再发送[**ndis\_状态\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)状态通知，其中包含[**NDIS\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)结构，后者又包含一个[**WWAN\_设备\_槽\_映射\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_slot_mapping_info)结构以指示当前映射状态。 即使设置的请求失败，也是如此。 用于\_WWAN\_设备\_槽的 OID 的设置请求的结构\_映射\_信息[**是\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)\_\_\_\_\_

下图说明了一个设置请求。

![槽映射集](images/multi-SIM_7_slotMappingSet.png)

<a name="remarks"></a>备注
-------

主机预计在第一次启动时，该调制解调器在插槽和执行器之间具有默认映射。 主机使用 OID\_WWAN\_设备\_槽执行设置操作，\_映射\_信息以定义绑定到每个执行器的槽。 主机需要调制解调器跨重新启动和删除/插入来维护映射。 此 OID 不特定于执行器，并且可以发送到设备上的任何 NDIS 实例。 它还可以查询当前映射，如上所示。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_状态\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-device-slot-mappings)

[**NDIS\_WWAN\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

[**NDIS\_WWAN\_集\_设备\_槽\_映射\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)

 

 




