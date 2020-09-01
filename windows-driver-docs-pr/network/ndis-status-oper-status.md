---
title: NDIS_STATUS_OPER_STATUS
description: "\"NDIS_STATUS_OPER_STATUS 状态\" 指示用于过量驱动程序的 NDIS 网络接口的当前操作状态。"
ms.assetid: dbe7ce19-290d-4a48-a6c2-1b95e956c26c
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_OPER_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bc4429963fb83bb7efb56a04262c2797e6662957
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214686"
---
# <a name="ndis_status_oper_status"></a>NDIS \_ 状态 \_ 操作系统 \_ 状态


"NDIS \_ 状态 \_ 操作系统 \_ 状态" 状态指示超出驱动程序的 ndis 网络接口的当前操作状态。

<a name="remarks"></a>备注
-------

NDIS 生成此状态指示;NDIS 微型端口驱动程序不应生成此状态指示。

NDIS 在[**ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员中提供了[**ndis \_ 操作系统 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_oper_state)结构。

[**Ndis \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBufferSize**成员设置为 sizeof (NDIS \_ 操作系统 \_ 状态) 。

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
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 操作系统 \_ 状态**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_oper_state)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

 

