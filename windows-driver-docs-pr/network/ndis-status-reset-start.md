---
title: NDIS_STATUS_RESET_START
description: NDIS_STATUS_RESET_START 状态指示正在重置微型端口适配器。
ms.assetid: 8758652b-137b-43e3-a896-8360f2b5051c
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RESET_START 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2c0a22f0fec7b6921edbd79195d271d28b59baa9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843516"
---
# <a name="ndis_status_reset_start"></a>NDIS\_状态\_RESET\_START


NDIS\_状态\_RESET\_START status 表明正在重置微型端口适配器。

<a name="remarks"></a>备注
-------

微型端口驱动程序不应调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数来通知每个重置操作的开始和完成，因为当重置操作开始和结束时，NDIS 会通知过量驱动程序。

当 NDIS 调用微型端口驱动程序的[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)函数时，微型端口驱动程序会重置微型端口适配器。 NDIS 调用每个绑定协议和中间驱动程序的[*ProtocolStatusEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)函数，并使用 NDIS\_状态\_RESET\_START 的状态为 NDIS 筛选器模块的[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)函数。 当微型端口驱动程序完成重置时，NDIS 会将具有 NDIS\_状态的过量驱动程序通知[ **\_reset\_END**](ndis-status-reset-end.md)。

如果协议驱动程序收到 NDIS\_状态\_RESET\_开始状态指示，则应执行以下操作：

-   保存准备好传输的所有数据，直到其*ProtocolStatusEx*函数接收到 NDIS\_状态\_RESET\_结束状态指示。

-   不要执行定向到基础微型端口驱动程序的任何 NDIS 调用，只需调用即可返回资源，例如，通过[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)函数返回接收的数据缓冲区。

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
<td>Ndis .h （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[*FilterStatus*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_status)

[*MiniportResetEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_reset)

[ **\_重置\_结尾的 NDIS\_状态**](ndis-status-reset-end.md)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

[**NdisReturnNetBufferLists**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreturnnetbufferlists)

[*ProtocolStatusEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_status_ex)

 

 




