---
title: OID_WWAN_SMS_DELETE
description: OID_WWAN_SMS_DELETE 将删除存储在 MB 设备或订阅服务器标识模块 (SIM 卡) 或任何其他辅助非易失性内存或内存的短信。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_DELETE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d5651e8b5afde3b88de23e978d8ed62a5c0020de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812907"
---
# <a name="oid_wwan_sms_delete"></a>OID \_ WWAN \_ SMS \_ 删除


OID \_ WWAN \_ SMS \_ DELETE 删除存储在 MB 设备或订户标识模块 (SIM 卡) 或任何其他辅助非易失性内存或内存中的短信。

不支持查询请求。

Set 请求使用 [**NDIS \_ WWAN \_ SMS \_ DELETE**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete) 结构。

微型端口驱动程序以异步方式处理此 OID，并应返回 NDIS \_ 状态 \_ 指示 \_ 需要对任何设置请求的临时响应。 小型端口驱动程序在完成事务后，应发送 [**NDIS \_ 状态 \_ WWAN \_ SMS \_ 删除**](ndis-status-wwan-sms-delete.md) 指示。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN SMS 操作](./mb-sms-operations.md)。

当处理此 OID 时，微型端口驱动程序可以 (SIM 卡) 访问订阅服务器标识模块，但不应访问提供程序的网络。

微型端口驱动程序可能会收到根据索引删除 SMS 文本消息的请求，或删除所有 SMS 文本消息的请求。 Delete 请求可能包含任何一种基本筛选器，例如 new (未读) 消息、旧 (读取) 消息、草稿消息或已发送消息。

如果微型端口驱动程序 \_ \_ \_ 不支持短信，或者无法删除 sms 文本消息，则它应返回不受支持的 NDIS 状态。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ SMS \_ 删除**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_delete)

[WWAN SMS 操作](./mb-sms-operations.md)

 

