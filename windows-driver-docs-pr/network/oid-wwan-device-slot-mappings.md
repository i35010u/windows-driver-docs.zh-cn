---
title: OID_WWAN_DEVICE_SLOT_MAPPING_INFO
description: OID_WWAN_DEVICE_SLOT_MAPPING_INFO 设置或返回 MB 设备的设备槽映射 (例如，执行器槽映射) 。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SLOT_MAPPING_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5c01de80b7810906c95ba380fe99d7f63bc1711c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797955"
---
# <a name="oid_wwan_device_slot_mapping_info"></a>OID \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息


OID \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息设置或返回 MB 设备的设备槽映射， (即执行器槽映射) 。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，然后再发送 [**ndis \_ 状态 \_ WWAN \_ 设备 \_ 槽 \_ \_**](./ndis-status-wwan-device-slot-mappings.md) 映射信息状态通知，其中包含 [**ndis \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info) 结构，以提供执行器到槽映射的信息。

下图演示了一个查询请求。

![槽映射查询](images/multi-SIM_8_slotMappingQuery.png)

微型端口驱动程序必须异步处理设置请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，然后再发送 [**ndis \_ 状态 \_ wwan \_ 设备 \_ \_ \_**](./ndis-status-wwan-device-slot-mappings.md) 槽映射信息状态通知，其中包含 [**ndis \_ wwan \_ 设备 \_ \_ \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info) 槽映射信息结构，后者又包含用于指示当前映射状态的 [**WWAN \_ 设备 \_ 槽 \_ \_**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_device_slot_mapping_info) 映射信息结构。 即使设置的请求失败，也是如此。 用于 OID \_ wwan 设备槽映射信息的集请求的结构 \_ \_ \_ \_ 为 [**NDIS \_ wwan \_ 设置 \_ 设备 \_ 槽 \_ 映射 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)。

下图说明了一个设置请求。

![槽映射集](images/multi-SIM_7_slotMappingSet.png)

<a name="remarks"></a>备注
-------

主机预计在第一次启动时，该调制解调器在插槽和执行器之间具有默认映射。 主机使用 OID \_ WWAN \_ 设备 \_ 槽映射信息执行 SET 操作 \_ \_ ，以定义绑定到每个执行器的槽。 主机需要调制解调器跨重新启动和删除/插入来维护映射。 此 OID 不特定于执行器，并且可以发送到设备上的任何 NDIS 实例。 它还可以查询当前映射，如上所示。

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
<td><p>Windows 10 版本 1703</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 状态 \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息**](./ndis-status-wwan-device-slot-mappings.md)

[**NDIS \_ WWAN \_ 设备 \_ 槽 \_ 映射 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_device_slot_mapping_info)

[**NDIS \_ WWAN \_ 设置 \_ 设备 \_ 槽 \_ 映射 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_device_slot_mapping_info)

 

