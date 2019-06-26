---
title: OID_WWAN_SLOT_INFO
description: OID_WWAN_SLOT_INFO 检索指定的 UICC 槽中，在其中 （如果有） 卡的高级聚合的状态。 它还可能用于一个槽的状态发生更改时提供的未经请求的通知。
ms.assetid: 6267D480-5055-4A7A-B2A0-F4DF9154DCD7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SLOT_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 38912dadac22a6f2e98363aea00e8904e14c70db
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383202"
---
# <a name="oidwwanslotinfo"></a>OID\_WWAN\_槽\_信息


OID\_WWAN\_槽\_信息检索指定的 UICC 槽中，在其中的卡的高级聚合的状态 （如果有）。 它还可能用于一个槽的状态发生更改时提供的未经请求的通知。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_需要更高版本在发送之前对原始请求[ **NDIS\_状态\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)状态通知包含[ **NDIS\_WWAN\_槽\_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)结构，其中又包含[ **WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_slot_info)结构，以提供有关的信息总体调制解调器系统功能。

指定查询请求[ **NDIS\_WWAN\_获取\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info)结构作为输入。 微型端口驱动程序应返回插槽的状态根据中指定 ID 的槽**SlotIndex**的成员[ **WWAN\_获取\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_get_slot_info)结构。

下图说明了查询请求。

![槽状态查询](images/multi-SIM_9_slotStatusQuery.png)

不适用集发出的请求。

[ **NDIS\_状态\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)通知[ **NDIS\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)结构发送到主机的槽/卡状态发生更改时。

<a name="remarks"></a>备注
-------

主机使用 OID\_WWAN\_槽\_要查询特定槽的调制解调器上的状态信息。 此 OID 不特定于执行器的可能会发送到任何 NDIS 实例属于一个调制解调器。 槽状态表示此槽和数据卡的状态的摘要。

报告的状态集被受槽硬件的功能。 在限制性最强的情况下，槽硬件可能仅能确定数据卡开机时存在且处于活动状态，这种情况下**OffEmpty**和**关闭**将不会报告状态。

[OID\_WWAN\_准备\_信息](oid-wwan-ready-info.md)和 OID\_WWAN\_槽\_信息执行检索 SIM 卡槽; 设备就绪状态的核心功能相同但 OID\_WWAN\_准备\_信息是每个执行器命令，而 OID\_WWAN\_槽\_信息可用于执行任何物理实例 （执行器） 和应返回即使它未映射到任何执行程序目前适当的插槽的状态。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_STATUS\_WWAN\_SLOT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)

[**NDIS\_WWAN\_SLOT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

[**WWAN\_SLOT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_slot_info)

[**NDIS\_WWAN\_GET\_SLOT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info)

[**WWAN\_GET\_SLOT\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ns-wwan-_wwan_get_slot_info)

[**WWAN\_UICCSLOT\_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wwan/ne-wwan-_wwan_uiccslot_state)

[OID\_WWAN\_READY\_INFO](oid-wwan-ready-info.md)

 

 




