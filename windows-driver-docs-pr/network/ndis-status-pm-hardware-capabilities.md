---
title: NDIS_STATUS_PM_HARDWARE_CAPABILITIES
description: NDIS_STATUS_PM_HARDWARE_CAPABILITIES 状态向过量驱动程序指出电源管理 (PM 中的更改) 了网络适配器的硬件功能。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_HARDWARE_CAPABILITIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5f92e666d3b3a04f960921bf9c7a0385d322e2cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801485"
---
# <a name="ndis_status_pm_hardware_capabilities"></a>NDIS \_ 状态 \_ PM \_ 硬件 \_ 功能


**NDIS \_ 状态 \_ PM \_ 硬件 \_ 功能** 状态指示过量驱动程序，电源管理 (PM 的更改) 网络适配器的硬件功能发生变化。

<a name="remarks"></a>备注
-------

当需要对以前报告的电源管理功能进行更新时，微型端口驱动程序将生成 **NDIS \_ 状态 \_ PM \_ 硬件 \_ 功能** 状态指示。

802.11 网络适配器的微型端口驱动程序可以生成此状态指示。

提供负载平衡故障转移 (LBFO) 支持的 MUX 中间驱动程序还可以生成此状态指示。 MUX 驱动程序聚合属于 LBFO 团队的基础网络适配器的 PM 功能。 如果 PM 功能发生更改，原因是已在团队中添加或删除适配器，则 MUX 驱动程序必须生成此状态指示。 有关 LBFO MUX 中间驱动程序的详细信息，请参阅 [NDIS Mux 中间驱动程序](./ndis-mux-intermediate-drivers.md)。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含一个指针，指向带有更新的电源管理功能的 [**ndis \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)结构。

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ PM \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pm_capabilities)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

