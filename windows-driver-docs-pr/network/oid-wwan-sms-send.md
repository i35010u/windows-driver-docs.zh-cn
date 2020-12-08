---
title: OID_WWAN_SMS_SEND
description: OID_WWAN_SMS_SEND 将短信发送给另一个 MB 设备。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_SEND 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 490b42846121c44d2dcb1ce012f8dfded8adccb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812897"
---
# <a name="oid_wwan_sms_send"></a>OID \_ WWAN \_ SMS \_ 发送


OID \_ WWAN \_ SMS \_ 发送向另一个 MB 设备发送短信。

不支持查询请求。

Set 请求使用 [**NDIS \_ WWAN \_ SMS \_ 发送**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send) 结构。

微型端口驱动程序以异步方式处理此 OID，并应返回 NDIS \_ 状态 \_ 指示 \_ 需要对任何设置请求的临时响应。 小型端口驱动程序在完成事务后，应发送 [**NDIS \_ 状态 \_ WWAN \_ SMS \_ 发送**](ndis-status-wwan-sms-send.md) 指示。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN SMS 操作](./mb-sms-operations.md)。

当处理此 OID 时，微型端口驱动程序可以访问提供程序网络，但不应 (SIM 卡) 访问订阅服务器标识模块。

OID \_ WWAN \_ sms \_ SEND 支持发送 PDU 模式和 CDMA 模式短信，具体取决于设备的功能。

基于 GSM 的设备应仅支持 PDU 模式短信。 基于 CDMA 的设备预计仅支持 CDMA 模式短信。 无需考虑 SMS 文本消息模式，微型端口驱动程序必须能够完成设置请求。

如果微型端口驱动程序 \_ \_ \_ 不支持短信或发送短信，则它应返回不受支持的 NDIS 状态。

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


[**NDIS \_ WWAN \_ SMS \_ 发送**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)

[WWAN SMS 操作](./mb-sms-operations.md)

 

