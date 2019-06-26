---
title: OID_WWAN_SMS_STATUS
description: OID_WWAN_SMS_STATUS 报告的 MB 设备的消息存储区的状态。
ms.assetid: a43451e6-f589-4963-acc7-855555655d37
ms.date: 08/08/2017
keywords: -OID_WWAN_SMS_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 91c1e0fcaa8d32bb5f484d05b57d09e83846b997
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384720"
---
# <a name="oidwwansmsstatus"></a>OID\_WWAN\_SMS\_状态


OID\_WWAN\_SMS\_状态报告的 MB 设备的消息存储区状态。

不支持组的请求。

查询的请求不使用一种结构。

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS\_状态\_指示\_原始请求和更高版本发送所需[ **NDIS\_状态\_WWAN\_SMS\_状态**](ndis-status-wwan-sms-status.md)指示状态的 MB 设备的消息存储区完成查询请求时的状态通知。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)。

在处理此 OID 时，微型端口驱动程序可以访问用户识别模块 （SIM 卡），但不是应访问提供程序网络。

微型端口驱动程序应返回 NDIS\_状态\_不\_如果它们不支持短信支持。

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


[WWAN SMS 操作](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sms-operations)

[**NDIS\_STATUS\_WWAN\_SMS\_STATUS**](ndis-status-wwan-sms-status.md)

 

 




