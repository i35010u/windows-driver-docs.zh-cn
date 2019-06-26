---
title: OID_WWAN_SMS_SEND
description: OID_WWAN_SMS_SEND 将短信发送到另一台的 MB 设备。
ms.assetid: 557d2bdc-8414-4fcb-903c-23bb68955d07
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_SEND 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 895b2e76ae38ea12b3fe9a5ecb2d6bf72fcefc79
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383186"
---
# <a name="oidwwansmssend"></a>OID\_WWAN\_SMS\_SEND


OID\_WWAN\_SMS\_发送到另一个的 MB 设备发送短信。

不支持查询请求。

设置请求使用[ **NDIS\_WWAN\_SMS\_发送**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)结构。

微型端口驱动程序以异步方式处理此 OID，并应返回 NDIS\_状态\_指示\_必需临时响应任何集请求。 微型端口驱动程序应发送[ **NDIS\_状态\_WWAN\_SMS\_发送**](ndis-status-wwan-sms-send.md)指示它们完成事务的时间。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)。

在处理此 OID 时，微型端口驱动程序可以访问提供程序网络，但不是应访问用户识别模块 （SIM 卡）。

OID\_WWAN\_SMS\_发送支持发送 PDU 模式和 CDMA 模式 SMS 文本消息，具体取决于设备的功能。

应基于 GSM 的设备支持仅 PDU 模式短信。 应基于 CDMA 的设备支持仅 CDMA 模式短信。 微型端口驱动程序必须能够完成而不考虑 SMS 文本消息模式的集请求。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持短信或发送短信的功能支持。

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
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_SMS\_SEND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_send)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




