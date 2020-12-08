---
title: NDIS_STATUS_PM_CAPABILITIES_CHANGE
description: "\"NDIS_STATUS_PM_CAPABILITIES_CHANGE 状态\" 指示网络适配器对过量驱动程序的电源管理功能发生了更改。"
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_PM_CAPABILITIES_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c94d594b920802a601371d70d24e6dc1e12c3900
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801495"
---
# <a name="ndis_status_pm_capabilities_change"></a>NDIS \_ 状态 \_ PM \_ 功能 \_ 更改


NDIS \_ 状态 \_ PM \_ 功能 \_ 更改状态表明网络适配器对过量驱动程序的电源管理功能发生了更改。

<a name="remarks"></a>备注
-------

\_ \_ \_ \_ 当需要对以前报告的电源管理功能进行更新时，ndis 将生成 ndis 状态 PM 功能更改状态指示。

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
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
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

 

