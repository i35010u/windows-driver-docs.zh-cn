---
title: OID_WWAN_SMS_SEND
description: OID_WWAN_SMS_SEND 将短信发送到另一台的 MB 设备。
ms.assetid: 557d2bdc-8414-4fcb-903c-23bb68955d07
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_SMS_SEND 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dfc0f9196d3aab2b6254f70e3ae435eeca1d145f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563193"
---
# <a name="oidwwansmssend"></a>OID\_WWAN\_SMS\_SEND


OID\_WWAN\_SMS\_发送到另一个的 MB 设备发送短信。

不支持查询请求。

设置请求使用[ **NDIS\_WWAN\_SMS\_发送**](https://msdn.microsoft.com/library/windows/hardware/ff567943)结构。

微型端口驱动程序以异步方式处理此 OID，并应返回 NDIS\_状态\_指示\_必需临时响应任何集请求。 微型端口驱动程序应发送[ **NDIS\_状态\_WWAN\_SMS\_发送**](ndis-status-wwan-sms-send.md)指示它们完成事务的时间。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)。

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
<td><p>版本</p></td>
<td><p>在 Windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_WWAN\_SMS\_SEND**](https://msdn.microsoft.com/library/windows/hardware/ff567943)

[WWAN SMS 操作](https://msdn.microsoft.com/library/windows/hardware/ff559131)

 

 




