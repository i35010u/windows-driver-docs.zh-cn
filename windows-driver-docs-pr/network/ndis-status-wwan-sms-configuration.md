---
title: NDIS_STATUS_WWAN_SMS_CONFIGURATION
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_CONFIGURATION 通知来通知 MB 服务有关上一个 OID_WWAN_SMS_CONFIGURATION \ 160; 查询或设置请求的完成，或在 SMS 配置发生更改的情况下通知 MB 服务。 小型端口驱动程序还可以通过此通知发送未经请求的事件。此通知使用 NDIS_WWAN_SMS_CONFIGURATION 结构。
ms.assetid: 86dfe2dc-070b-43d9-b6fa-54dee985c65d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_CONFIGURATION 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: eff450dab202f034ab3265c740710204bd6b1275
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216610"
---
# <a name="ndis_status_wwan_sms_configuration"></a>NDIS \_ 状态 \_ WWAN \_ SMS \_ 配置


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ sms \_ 配置通知来通知 MB 服务有关上一个[OID \_ WWAN \_ sms \_ 配置](oid-wwan-sms-configuration.md)   查询或设置请求的完成，或在 SMS 配置发生更改时的事件通知。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ SMS \_ 配置**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration) 结构。

<a name="remarks"></a>备注
-------

当 MB 设备的 SMS 子系统准备好执行 SMS 操作时，微型端口驱动程序必须发送此未经请求的指示。

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
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[OID \_ WWAN \_ SMS \_ 配置](oid-wwan-sms-configuration.md)

[**NDIS \_ WWAN \_ SMS \_ 配置**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_configuration)

 

