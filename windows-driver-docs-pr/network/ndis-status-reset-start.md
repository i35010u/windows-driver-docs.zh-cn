---
title: NDIS_STATUS_RESET_START
description: NDIS_STATUS_RESET_START 状态指示微型端口适配器将重置。
ms.assetid: 8758652b-137b-43e3-a896-8360f2b5051c
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RESET_START 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d258406610c2e42053e05099736a4661b73c6fa3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385080"
---
# <a name="ndisstatusresetstart"></a>NDIS\_状态\_重置\_开始


NDIS\_状态\_重置\_开始状态指示微型端口适配器将重置。

<a name="remarks"></a>备注
-------

微型端口驱动程序不应调用[ **NdisMIndicateStatusEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)函数来通知系统启动和完成的每个重置操作，因为 NDIS 重置操作开始时通知基础驱动程序和结束。

时 NDIS 调用微型端口驱动程序微型端口驱动程序微型端口适配器重置[ *MiniportResetEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)函数。 NDIS 调用[ *ProtocolStatusEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)函数的每个绑定协议和中间驱动程序并[ *FilterStatus* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)的函数与的 NDIS 状态的基础筛选器模块\_状态\_重置\_开始。 NDIS 微型端口驱动程序完成后重置，通知的状态的基础驱动程序[ **NDIS\_状态\_重置\_最终**](ndis-status-reset-end.md)。

当协议驱动程序收到 NDIS\_状态\_重置\_开始状态指示它应：

-   保存已准备好之前传输任何数据，其*ProtocolStatusEx*函数接收 NDIS\_状态\_重置\_最终状态指示。

-   不调用任何 NDIS 定向到的基础的微型端口驱动程序，但调用返回的资源，例如接收到数据缓冲区[ **NdisReturnNetBufferLists** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)函数。

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
<td><p>支持 Windows Vista 中的 NDIS 6.0 和 NDIS 5.1 驱动程序。 支持 NDIS 5.1 在 Windows XP 中的驱动程序。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_status)

[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_reset)

[**NDIS\_状态\_重置\_结束**](ndis-status-reset-end.md)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismindicatestatusex)

[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisreturnnetbufferlists)

[*ProtocolStatusEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_status_ex)

 

 




