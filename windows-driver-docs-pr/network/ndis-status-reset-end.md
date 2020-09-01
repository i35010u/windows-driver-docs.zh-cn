---
title: NDIS_STATUS_RESET_END
description: NDIS_STATUS_RESET_END 状态表明微型端口适配器重置操作已完成。
ms.assetid: 09ced263-9e4b-45e3-ae5e-db033a03b5b6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RESET_END 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 3c60d37a058d37887a493bcba8066bde08b87787
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206071"
---
# <a name="ndis_status_reset_end"></a>NDIS \_ 状态 \_ 重置 \_ 结束


NDIS \_ 状态 \_ 重置 \_ 结束状态表明微型端口适配器重置操作已完成。

<a name="remarks"></a>备注
-------

微型端口驱动程序不应调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 函数来通知每个重置操作的开始和完成，因为当重置操作开始和结束时，NDIS 会通知过量驱动程序。

当微型端口驱动程序启动重置操作时，NDIS 将使用 [**ndis \_ 状态 \_ 重置 \_ 开始**](ndis-status-reset-start.md) 状态指示通知过量驱动程序。

绑定协议驱动程序收到 NDIS \_ 状态 \_ 重置 \_ 结束状态指示后，协议驱动程序可以继续发送数据并发出 OID 请求。

当过量筛选器或中间驱动程序收到 NDIS \_ 状态 \_ 重置 \_ 结束状态指示之后，驱动程序可以继续发送数据，并向过量驱动程序发出 OID 请求。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 Windows XP 中的 NDIS 5.1 驱动程序支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ 状态 \_ 重置 \_ 启动**](ndis-status-reset-start.md)

[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

