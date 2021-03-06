---
title: NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 状态指示通知 NDIS 和过量驱动程序已在封装设置中发生了更改。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fcc61a82f8366035055c432296736e0d72f27f3f
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102249259"
---
# <a name="ndis_status_offload_encaspulation_change"></a>NDIS \_ 状态 \_ 卸载 \_ ENCASPULATION \_ 更改


微型端口驱动程序使用 NDIS \_ 状态 \_ 卸载 \_ ENCASPULATION \_ 更改状态指示通知 ndis 和过量驱动程序已在封装设置中发生了更改。

<a name="remarks"></a>备注
-------

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的 **StatusBuffer** 成员包含 [**ndis \_ 卸载 \_ 封装**](/windows-hardware/drivers/ddi/encapsulationconfig/ns-encapsulationconfig-ndis_offload_encapsulation)结构。 NDIS \_ 卸载 \_ 封装指定了封装设置。

有关封装设置的详细信息，请参阅 [OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md)。

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
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标题</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 卸载 \_ 封装**](/windows-hardware/drivers/ddi/encapsulationconfig/ns-encapsulationconfig-ndis_offload_encapsulation)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ 卸载 \_ 封装](./oid-offload-encapsulation.md)

 

