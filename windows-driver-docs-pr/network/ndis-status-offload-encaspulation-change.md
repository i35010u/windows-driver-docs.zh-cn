---
title: NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE
description: 微型端口驱动程序使用 NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 状态指示通知 NDIS 和过量驱动程序已在封装设置中发生了更改。
ms.assetid: 2db2a42e-85a2-41a6-b6ab-13b493057648
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_OFFLOAD_ENCASPULATION_CHANGE 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3055200cc8aded2fabfdd37773e78c666b45d1f3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842778"
---
# <a name="ndis_status_offload_encaspulation_change"></a>\_卸载\_ENCASPULATION\_更改的 NDIS\_状态


微型端口驱动程序使用 NDIS\_状态\_卸载\_ENCASPULATION\_更改状态指示，通知 NDIS 和过量驱动程序已在封装设置中发生了更改。

<a name="remarks"></a>备注
-------

[**Ndis\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的**StatusBuffer**成员包含[**ndis\_卸载\_封装**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)结构。 NDIS\_卸载\_封装指定了封装设置。

有关封装设置的详细信息，请参阅[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[ **\_封装的 NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_offload_encapsulation)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID\_卸载\_封装](https://docs.microsoft.com/windows-hardware/drivers/network/oid-offload-encapsulation)

 

 




