---
title: OID_WWAN_SMS_CONFIGURATION
description: OID_WWAN_SMS_CONFIGURATION 设置或返回一个 MB 设备的 SMS 文本消息配置。
ms.assetid: 3292a91d-4aa8-4c57-9223-d7d984dc5d69
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_CONFIGURATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 95ad11e107489620a7037e5e23a8327b970c210b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843788"
---
# <a name="oid_wwan_sms_configuration"></a>OID\_WWAN\_SMS\_配置


OID\_WWAN\_SMS\_配置设置或返回 MB 设备的 SMS 文本消息配置。

微型端口驱动程序必须异步处理集和查询请求，最初返回 NDIS\_状态\_指示\_需要原始请求，稍后将[**ndis\_状态\_WWAN\_SMS 发送\_配置**](ndis-status-wwan-sms-configuration.md)状态通知，与完成的集或查询请求无关。

查询请求返回设备或订阅服务器标识模块（SIM）卡中存储的 MB 设备的当前 SMS 文本消息配置。

设置请求使用[**NDIS\_WWAN\_设置\_sms\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)结构来更改 MB 设备的 sms 文本消息配置。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)。

当处理此 OID 时，微型端口驱动程序可以访问 SIM 卡，但不应访问提供程序网络。

基于 GSM 的设备的微型端口驱动程序应支持查询和设置操作。 基于 CDMA 的设备的微型端口驱动程序应仅支持查询操作。 基于 CDMA 的设备的微型端口驱动程序应在查询请求的 WWAN\_SMS\_配置结构的**ulMaxMessageIndex**成员中返回有效的值，并且可以忽略其他成员。

小型端口驱动程序必须在 MB 设备的 SMS 子系统准备好执行 SMS 操作时，将未经请求的 NDIS\_状态\_WWAN\_SMS\_配置指示。 此后，当响应 OID\_WWAN\_SMS\_配置查询请求时，微型端口驱动程序必须为 WWAN\_SMS\_配置结构的所有成员返回有效值。

如果设备已初始化但 SMS 子系统尚未初始化，微型端口驱动程序应返回 NDIS\_状态\_未\_初始化。

如果不支持配置 SMS 文本消息，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

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


[**NDIS\_WWAN\_设置\_SMS\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sms_configuration)

[**WWAN\_SMS\_配置\_的 NDIS\_状态**](ndis-status-wwan-sms-configuration.md)

[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

 

 




