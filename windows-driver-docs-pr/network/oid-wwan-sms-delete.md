---
title: OID_WWAN_SMS_DELETE
description: OID_WWAN_SMS_DELETE 删除存储在 MB 设备或订阅服务器标识模块（SIM 卡）或任何其他辅助非易失性内存或内存中的短信。
ms.assetid: b80fae94-35cc-4709-8346-d5a500d3fd49
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_DELETE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ee57b0347db462fd9eb94f1faeda48d64bce9d68
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843786"
---
# <a name="oid_wwan_sms_delete"></a>OID\_WWAN\_SMS\_删除


OID\_WWAN\_SMS\_删除删除存储在 MB 设备或订阅服务器标识模块（SIM 卡）或任何其他辅助非易失性内存或内存中的 SMS 文本消息。

不支持查询请求。

设置请求使用[**NDIS\_WWAN\_SMS\_删除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete)结构。

微型端口驱动程序以异步方式处理此 OID，并应返回 NDIS\_状态\_指示\_需要对任何设置请求的临时响应。 小型端口驱动程序应将[**NDIS\_状态\_WWAN\_SMS\_** ](ndis-status-wwan-sms-delete.md)在其完成该事务时删除指示。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)。

当处理此 OID 时，微型端口驱动程序可以访问订阅服务器标识模块（SIM 卡），但不应访问提供商的网络。

微型端口驱动程序可能会收到根据索引删除 SMS 文本消息的请求，或删除所有 SMS 文本消息的请求。 删除请求可能包含任何一种基本筛选器，例如新的（未读）消息、旧的（读取）消息、草稿消息或发送的消息。

如果不支持短信或删除短信的功能，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_WWAN\_SMS\_删除**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




