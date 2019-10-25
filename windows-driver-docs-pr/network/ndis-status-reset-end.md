---
title: NDIS_STATUS_RESET_END
description: NDIS_STATUS_RESET_END 状态指示微型端口适配器重置操作已完成。
ms.assetid: 09ced263-9e4b-45e3-ae5e-db033a03b5b6
ms.date: 07/18/2017
keywords:
- NDIS_STATUS_RESET_END 从 Windows Vista 开始的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7583fd7db8c73eae0009f2fd2e4477bab841e4bf
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843518"
---
# <a name="ndis_status_reset_end"></a>\_重置\_结尾的 NDIS\_状态


NDIS\_状态\_RESET\_结束状态表明微型端口适配器重置操作已完成。

<a name="remarks"></a>备注
-------

微型端口驱动程序不应调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)函数来通知每个重置操作的开始和完成，因为当重置操作开始和结束时，NDIS 会通知过量驱动程序。

当微型端口驱动程序启动重置操作时，NDIS 会将具有 NDIS\_状态的过量驱动程序通知[ **\_reset\_开始**](ndis-status-reset-start.md)状态指示。

绑定协议驱动程序接收到 NDIS\_状态\_RESET\_结束状态指示后，协议驱动程序可以继续发送数据和发出 OID 请求。

当过量筛选器或中间驱动程序收到 NDIS\_状态\_RESET\_结束状态指示之后，驱动程序可以继续发送数据，并向过量驱动程序发出 OID 请求。

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


[**NDIS\_状态\_RESET\_START**](ndis-status-reset-start.md)

[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)

 

 




