---
title: OID_WWAN_SMS_CONFIGURATION
description: OID_WWAN_SMS_CONFIGURATION 设置或返回 MB 设备的 SMS 文本消息配置。
ms.assetid: 3292a91d-4aa8-4c57-9223-d7d984dc5d69
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_CONFIGURATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f285c21c3b0bc8010de3beb3493e13ddb44eeae9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361171"
---
# <a name="oidwwansmsconfiguration"></a>OID\_WWAN\_SMS\_配置


OID\_WWAN\_SMS\_配置设置或返回 MB 设备的 SMS 文本消息配置。

微型端口驱动程序必须处理集和查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_SMS\_配置**](ndis-status-wwan-sms-configuration.md)而不考虑完成集或查询请求的状态通知。

查询请求返回 MB 设备的当前 SMS 文本消息配置存储在设备或订阅服务器上标识模块 (SIM) 卡。

设置请求使用[ **NDIS\_WWAN\_设置\_SMS\_CONFIGURATION** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)结构，以更改 SMS 文本消息配置的 MB 设备.

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)。

在处理此 OID 时，微型端口驱动程序可以访问 SIM 卡，但不是应访问提供程序网络。

基于 GSM 的设备的微型端口驱动程序应支持这两个查询和设置操作。 基于 CDMA 的设备的微型端口驱动程序应支持仅查询操作。 基于 CDMA 的设备的微型端口驱动程序应返回中的有效值**ulMaxMessageIndex** WWAN 成员\_SMS\_配置结构的查询请求，并且可以忽略其他成员。

微型端口驱动程序必须发送未经请求的 NDIS\_状态\_WWAN\_SMS\_配置指示 MB 设备的短信子系统可供 SMS 操作时。 此后，响应 OID 时\_WWAN\_SMS\_配置查询请求时，微型端口驱动程序的所有成员 WWAN 必须返回有效的值\_SMS\_配置结构。

微型端口驱动程序应返回 NDIS\_状态\_不\_初始化如果设备已初始化，但尚未初始化的短信子系统。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持配置短信支持。

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


[**NDIS\_WWAN\_SET\_SMS\_CONFIGURATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)

[**NDIS\_状态\_WWAN\_SMS\_配置**](ndis-status-wwan-sms-configuration.md)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




