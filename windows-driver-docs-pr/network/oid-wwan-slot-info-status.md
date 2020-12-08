---
title: OID_WWAN_SLOT_INFO
description: OID_WWAN_SLOT_INFO 检索指定 UICC 槽的高级聚合状态和其中的卡 (如果任何) ，则为。 当某个槽的状态发生更改时，也可以使用它来传递未经请求的通知。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SLOT_INFO 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1dac31e5ecc51d6d2f250098bec03b9f3ea7c3b4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812915"
---
# <a name="oid_wwan_slot_info"></a>OID \_ WWAN \_ 槽 \_ 信息


OID \_ WWAN \_ 槽 \_ 信息检索指定 UICC 槽的高级汇总状态，其中的卡 (如果任何) ，则为。 当某个槽的状态发生更改时，也可以使用它来传递未经请求的通知。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，然后再发送一个包含 [**ndis \_ wwan \_ \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)槽信息状态通知的 ndis [**\_ 状态 \_ wwan \_ 槽 \_**](./ndis-status-wwan-slot-info-status.md)信息状态通知，后者又包含一个 [**wwan \_ 槽 \_**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_slot_info)信息结构，用于提供有关调制解调器总体系统功能的信息。

查询请求将 [**NDIS \_ WWAN \_ 获取 \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info) 结构指定为输入。 微型端口驱动程序应根据 [**WWAN \_ 获取 \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_get_slot_info)结构的 **SLOTINDEX** 成员中指定的槽 ID 返回槽状态。

下图演示了一个查询请求。

![槽状态查询](images/multi-SIM_9_slotStatusQuery.png)

设置请求不适用。

当槽/插卡状态发生变化时，会将 [**ndis \_ 状态 \_ wwan \_ 槽 \_ 信息**](./ndis-status-wwan-slot-info-status.md) 通知发送到 [**ndis \_ WWAN \_ 槽 \_**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info) 信息结构。

<a name="remarks"></a>备注
-------

主机使用 OID \_ WWAN \_ 插槽 \_ 信息来查询调制解调器上特定插槽的状态。 此 OID 不特定于执行器，并且可以发送到属于一个调制解调器的任何 NDIS 实例。 槽状态表示槽和卡状态的摘要。

报告的状态集受插槽硬件功能的限制。 在最严格的情况下，槽硬件可能只有在电源打开且处于活动状态时才能确定卡是否存在，在这种情况下，将不报告 **OffEmpty** 和 **Off** 状态。

[OID \_WWAN \_ 就绪 \_ 信息](oid-wwan-ready-info.md) 和 OID \_ wwan \_ 槽 \_ 信息执行检索设备就绪状态的相同核心功能，即 SIM 卡槽的状态; 但是，oid \_ wwan \_ 就绪 \_ 信息是按执行器的信息，而 oid \_ wwan \_ 槽 \_ 信息可以在任何物理实例上用于 (执行器) 并且应返回合适的槽状态，即使当时未映射到任何执行器也是如此。

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


[**NDIS \_ 状态 \_ WWAN \_ 槽 \_ 信息**](./ndis-status-wwan-slot-info-status.md)

[**NDIS \_ WWAN \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_slot_info)

[**WWAN \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_slot_info)

[**NDIS \_ WWAN \_ 获取 \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_get_slot_info)

[**WWAN \_ 获取 \_ 槽 \_ 信息**](/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_get_slot_info)

[**WWAN \_ UICCSLOT \_ 状态**](/windows-hardware/drivers/ddi/wwan/ne-wwan-_wwan_uiccslot_state)

[OID \_ WWAN \_ 就绪 \_ 信息](oid-wwan-ready-info.md)

 

