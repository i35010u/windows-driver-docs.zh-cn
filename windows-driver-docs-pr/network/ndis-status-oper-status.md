---
title: NDIS_STATUS_OPER_STATUS
description: NDIS_STATUS_OPER_STATUS 状态指示过量驱动程序的 NDIS 网络接口的当前操作状态。
ms.assetid: dbe7ce19-290d-4a48-a6c2-1b95e956c26c
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_OPER_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f303b176eb45e2792d88a6bbe19bf693c90610b6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368559"
---
# <a name="ndisstatusoperstatus"></a>NDIS\_状态\_工序\_状态


NDIS\_状态\_工序\_状态状态指示过量驱动程序的 NDIS 网络接口的当前操作状态。

<a name="remarks"></a>备注
-------

NDIS 生成此状态指示;NDIS 微型端口驱动程序不应生成此状态指示。

NDIS 提供[ **NDIS\_工序\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_oper_state)结构**StatusBuffer**隶属[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构。

**StatusBufferSize**的成员[ **NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)结构设置为 sizeof (NDIS\_运算符\_状态）。

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
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_工序\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_oper_state)

[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_status_indication)

 

 




