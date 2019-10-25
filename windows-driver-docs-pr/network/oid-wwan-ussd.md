---
title: OID_WWAN_USSD
description: OID_WWAN_USSD 将非结构化补充服务数据（USSD）请求发送到基础 MB 设备。
ms.assetid: 9DFAAABD-8213-4B83-8FE8-1EC2BB9F735B
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_USSD 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 822ebc8f8ea000704c2a5ba85634cd494b32e93e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843766"
---
# <a name="oid_wwan_ussd"></a>OID\_WWAN\_USSD


OID\_WWAN\_USSD 将非结构化补充服务数据（USSD）请求发送到基础 MB 设备。

不支持查询请求。

微型端口驱动程序必须异步处理设置请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[ndis\_状态\_WWAN\_USSD](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)状态通知，其中包含初始 USSD 请求在完成该事务时的状态。

如果以前的请求仍在进行，则 Windows 不会将\_WWAN\_USSD 请求的 OID 发送到微型端口驱动程序，但通过设置[WWAN\_USSD\_请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request)**来取消挂起的操作除外。** 向*WwanUssdRequestCancel*请求的 RequestType 成员。

当请求被取消时，微型端口驱动程序必须响应取消的请求和取消请求。

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
<td><p>从 Windows 8 开始支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[WWAN\_USSD\_NDIS\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-wwan-ussd)

[WWAN\_USSD\_请求](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ussd_request)

 

 




