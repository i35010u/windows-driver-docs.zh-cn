---
title: OID_WWAN_SMS_STATUS
description: OID_WWAN_SMS_STATUS 报告 MB 设备的消息存储的状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a923cc5c8d86c2adab3ea30a6893c9afbfa2766f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812893"
---
# <a name="oid_wwan_sms_status"></a>OID \_ WWAN \_ SMS \_ 状态


OID \_ WWAN \_ SMS \_ 状态报告 MB 设备的消息存储的状态。

不支持设置请求。

查询请求不使用结构。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**NDIS \_ 状态 \_ WWAN \_ SMS \_ 状态**](ndis-status-wwan-sms-status.md) 通知，该通知指示完成查询请求时，MB 设备的消息存储区的状态。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN SMS 操作](./mb-sms-operations.md)。

当处理此 OID 时，微型端口驱动程序可以 (SIM 卡) 访问订阅服务器标识模块，但不应访问提供程序网络。

如果微型端口驱动程序 \_ 不 \_ \_ 支持短信，则它应返回不受支持的 NDIS 状态。

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


[WWAN SMS 操作](./mb-sms-operations.md)

[**NDIS \_ 状态 \_ WWAN \_ SMS \_ 状态**](ndis-status-wwan-sms-status.md)

 

