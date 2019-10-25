---
title: OID_WWAN_SMS_SEND
description: OID_WWAN_SMS_SEND 将短信发送给另一个 MB 设备。
ms.assetid: 557d2bdc-8414-4fcb-903c-23bb68955d07
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_SEND 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6e06857ffcba24dcc15ca621990a95ba95427d7e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843781"
---
# <a name="oid_wwan_sms_send"></a>OID\_WWAN\_SMS\_发送


OID\_WWAN\_SMS\_发送向另一个 MB 设备发送短信。

不支持查询请求。

设置请求使用[**NDIS\_WWAN\_SMS\_发送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)结构。

微型端口驱动程序以异步方式处理此 OID，并应返回 NDIS\_状态\_指示\_需要对任何设置请求的临时响应。 小型端口驱动程序应将[**NDIS\_状态\_WWAN\_SMS\_** ](ndis-status-wwan-sms-send.md)在其完成该事务时发送指示。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)。

当处理此 OID 时，微型端口驱动程序可以访问提供程序网络，但不应访问订阅服务器标识模块（SIM 卡）。

OID\_WWAN\_SMS\_SEND 支持发送 PDU 模式和 CDMA 短信，这取决于设备的功能。

基于 GSM 的设备应仅支持 PDU 模式短信。 基于 CDMA 的设备预计仅支持 CDMA 模式短信。 无需考虑 SMS 文本消息模式，微型端口驱动程序必须能够完成设置请求。

如果不支持短信或发送短信的功能，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

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


[**NDIS\_WWAN\_SMS\_发送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




