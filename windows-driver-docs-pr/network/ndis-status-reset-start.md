---
title: NDIS_STATUS_RESET_START
description: NDIS_STATUS_RESET_START 状态表明正在重置微型端口适配器。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RESET_START 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2b211219503e7ffce249820b8e11937c06a0c15a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801463"
---
# <a name="ndis_status_reset_start"></a>NDIS \_ 状态 \_ 重置 \_ 启动


NDIS \_ 状态 \_ 重置 \_ 开始状态表明正在重置微型端口适配器。

<a name="remarks"></a>备注
-------

微型端口驱动程序不应调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex) 函数来通知每个重置操作的开始和完成，因为当重置操作开始和结束时，NDIS 会通知过量驱动程序。

当 NDIS 调用微型端口驱动程序的 [*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset) 函数时，微型端口驱动程序会重置微型端口适配器。 NDIS 调用每个绑定协议和中间驱动程序的 [*ProtocolStatusEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)函数，并调用具有 NDIS [*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status) \_ 状态 \_ 重置启动状态的过量筛选器模块的 FilterStatus 函数 \_ 。 当微型端口驱动程序完成重置后，NDIS 会将状态 [**设置为 ndis \_ 状态 \_ 重置 \_ 结束**](ndis-status-reset-end.md)，并通知过量驱动程序。

当协议驱动程序收到 NDIS \_ 状态 \_ 重置 \_ 开始状态指示时，应执行以下操作：

-   保存准备好传输的所有数据，直到其 *ProtocolStatusEx* 函数收到 NDIS \_ 状态 \_ 重置 \_ 结束状态指示。

-   不要执行定向到基础微型端口驱动程序的任何 NDIS 调用，只需调用即可返回资源，例如，通过 [**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists) 函数返回接收的数据缓冲区。

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

## <a name="see-also"></a>请参阅


[*FilterStatus*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)

[*MiniportResetEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)

[**NDIS \_ 状态 \_ 重置 \_ 结束**](ndis-status-reset-end.md)

[**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[**NdisReturnNetBufferLists**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)

[*ProtocolStatusEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)

 

