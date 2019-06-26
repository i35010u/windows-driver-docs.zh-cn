---
title: NDIS_STATUS_WWAN_SMS_CONFIGURATION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_CONFIGURATION 通知来告知以前 OID_WWAN_SMS_CONFIGURATION 完成 MB 服务 \ 160; 查询或集请求或在发生更改时在 SMS 中的事件通知配置。 微型端口驱动程序还可以发送未经请求的事件与该通知。此通知使用 NDIS_WWAN_SMS_CONFIGURATION 结构。
ms.assetid: 86dfe2dc-070b-43d9-b6fa-54dee985c65d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_CONFIGURATION 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bb3f97a1dcad87fb73eadfcb4a88c1dfa6b9d48f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386858"
---
# <a name="ndisstatuswwansmsconfiguration"></a>NDIS\_状态\_WWAN\_SMS\_配置


微型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_配置通知，以通知 MB 服务有关的上一次完成[OID\_WWAN\_短信\_CONFIGURATION](oid-wwan-sms-configuration.md) 查询或 SMS 配置中设置请求或在发生更改时的事件通知。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_SMS\_配置**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)结构。

<a name="remarks"></a>备注
-------

SMS 操作准备就绪 MB 设备的短信子系统时，微型端口驱动程序必须发送此未经请求的指示。

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
<td>Ndis.h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID\_WWAN\_SMS\_CONFIGURATION](oid-wwan-sms-configuration.md)

[**NDIS\_WWAN\_SMS\_CONFIGURATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)

 

 




