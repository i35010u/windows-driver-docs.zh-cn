---
title: OID_WWAN_SLOT_INFO
description: OID_WWAN_SLOT_INFO 检索指定的 UICC 槽及其内的卡（如果有）的高级别聚合状态。 当某个槽的状态发生更改时，也可以使用它来传递未经请求的通知。
ms.assetid: 6267D480-5055-4A7A-B2A0-F4DF9154DCD7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SLOT_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5d6d360c02668fd352ca0847287fb254b1291a31
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843790"
---
# <a name="oid_wwan_slot_info"></a>OID\_WWAN\_槽\_信息


OID\_WWAN\_槽\_信息检索指定 UICC 槽及其内的卡（如果有）的高级别聚合状态。 当某个槽的状态发生更改时，也可以使用它来传递未经请求的通知。

微型端口驱动程序必须异步处理查询请求，最初返回 NDIS\_状态\_指示\_需要请求原始请求，然后再发送[**ndis\_状态\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)状态通知，其中包含一个[**NDIS\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)结构，后者又包含一个[**WWAN\_槽\_info**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_slot_info)结构，以提供有关整个调制解调器系统的信息功能.

查询请求指定[**NDIS\_WWAN\_获取\_槽作为输入\_槽**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info)。 微型端口驱动程序应根据[**WWAN\_获取\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_get_slot_info)结构中指定**的槽**ID 返回槽状态。

下图演示了一个查询请求。

![槽状态查询](images/multi-SIM_9_slotStatusQuery.png)

设置请求不适用。

当槽/插卡状态发生变化时， [**ndis\_状态\_wwan\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)通知，并将[**ndis\_wwan**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)\_的信息结构发送到主机。

<a name="remarks"></a>备注
-------

主机使用 OID\_WWAN\_槽\_信息在调制解调器上查询特定插槽的状态。 此 OID 不特定于执行器，并且可以发送到属于一个调制解调器的任何 NDIS 实例。 槽状态表示槽和卡状态的摘要。

报告的状态集受插槽硬件功能的限制。 在最严格的情况下，槽硬件可能只有在电源打开且处于活动状态时才能确定卡是否存在，在这种情况下，将不报告**OffEmpty**和**Off**状态。

[Oid\_wwan\_准备好\_信息](oid-wwan-ready-info.md)和 OID\_WWAN\_槽\_信息执行检索设备就绪状态的相同核心功能，即 SIM 卡槽的状态;但是，OID\_WWAN\_就绪\_信息是按执行器的命令，而 OID\_WWAN\_槽\_可以在任何物理实例（执行程序）上使用，并且应返回合适的槽状态，即使它不是当前映射到任何执行器。

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


[ **\_WWAN\_槽\_信息的 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-slot-info-status)

[**NDIS\_WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

[**WWAN\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_slot_info)

[**NDIS\_WWAN\_获取\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info)

[**WWAN\_获取\_槽\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_get_slot_info)

[**WWAN\_UICCSLOT\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_uiccslot_state)

[OID\_WWAN\_就绪\_信息](oid-wwan-ready-info.md)

 

 




