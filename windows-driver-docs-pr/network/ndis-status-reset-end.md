---
title: NDIS_STATUS_RESET_END
description: NDIS_STATUS_RESET_END 状态表明微型端口适配器重置操作已完成。
ms.assetid: 09ced263-9e4b-45e3-ae5e-db033a03b5b6
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_STATUS_RESET_END 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1c6c344047bde049e87f03fd2edcc02590703a0b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353162"
---
# <a name="ndisstatusresetend"></a>NDIS\_状态\_重置\_结束


NDIS\_状态\_重置\_最终状态表明微型端口适配器重置操作已完成。

<a name="remarks"></a>备注
-------

微型端口驱动程序不应调用[ **NdisMIndicateStatusEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563600)函数来通知系统启动和完成的每个重置操作，因为 NDIS 重置操作开始时通知基础驱动程序和结束。

NDIS 微型端口驱动程序启动时重置操作，会使用过量的驱动程序通知[ **NDIS\_状态\_重置\_启动**](ndis-status-reset-start.md)状态指示。

后一种绑定协议驱动程序将收到 NDIS\_状态\_重置\_最终状态指示协议驱动程序可以继续发送数据并发出 OID 请求。

基础筛选器或中间驱动程序收到 NDIS 后\_状态\_重置\_最终状态指示，该驱动程序可以继续发送数据并发出 OID 请求到过量驱动程序。

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


[**NDIS\_状态\_重置\_开始**](ndis-status-reset-start.md)

[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)

 

 




