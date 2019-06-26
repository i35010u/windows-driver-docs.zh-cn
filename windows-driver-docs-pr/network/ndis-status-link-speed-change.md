---
title: NDIS_STATUS_LINK_SPEED_CHANGE
description: NDIS_STATUS_LINK_SPEED_CHANGE 状态指示链接速度更改。
ms.assetid: 084e43c9-598c-4c30-8004-2d1876a1cddd
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_LINK_SPEED_CHANGE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 50025c65d233ce489acf3d2fd5c4b867ff15d9e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368575"
---
# <a name="ndisstatuslinkspeedchange"></a>NDIS\_状态\_链接\_速度\_更改


NDIS\_状态\_链接\_速度\_更改状态指示链接速度更改。

<a name="remarks"></a>备注
-------

NDIS 转换 NDIS\_状态\_链接\_速度\_更改为的状态指示[ **NDIS\_状态\_链接\_状态**](ndis-status-link-state.md)状态指示为过量 NDIS 6.0 驱动程序。 当 NDIS 收到 NDIS\_状态\_链接\_速度\_更改状态 NDIS 颁发的 OID 查询请求[OID\_常规\_链接\_速度](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed). NDIS 使用 OID 的结果\_GEN\_链接\_速度查询发出 NDIS\_状态\_链接\_状态状态设置为过量 NDIS 6.0 驱动程序。

NDIS 5。*x*或更早的微型端口驱动程序提供的 DWORD 类型值*StatusBuffer*参数[ **NdisMIndicateStatus** ](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))函数。 详细了解 NDIS\_状态\_链接\_速度\_更改，请参阅[OID\_IRDA\_速率\_探查](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560287(v=vs.85))。

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
<td><p>不受支持 NDIS 6.0 及更高版本 (使用<a href="ndis-status-link-state.md" data-raw-source="[&lt;strong&gt;NDIS_STATUS_LINK_STATE&lt;/strong&gt;](ndis-status-link-state.md)"> <strong>NDIS_STATUS_LINK_STATE</strong> </a>相反)。 仅支持 Windows Vista 和 Windows XP 中的 NDIS 5.1 驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_STATUS\_LINK\_STATE**](ndis-status-link-state.md)

[**NdisMIndicateStatus**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff553538(v=vs.85))

[OID\_GEN\_LINK\_SPEED](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-link-speed)

[OID\_IRDA\_RATE\_SNIFF](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff560287(v=vs.85))

 

 




