---
title: NDIS_STATUS_WWAN_SMS_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_STATUS 通知来通知 MB 服务以下事件 MB 设备的消息存储已满。新的 SMS 文本消息已到达，新消息与 MessageIndex 驱动程序相对应，还可以使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_SMS_STATUS 结构。
ms.assetid: 65553a3f-57af-49ef-a3b7-ed35df0a319d
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ce00553a17a3398f2f3ff20a43a967860039fcd3
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844630"
---
# <a name="ndis_status_wwan_sms_status"></a>\_WWAN\_SMS\_状态的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_状态通知来通知 MB 服务有关以下事件：

-   MB 设备的消息存储已满。

-   已到达新的短信消息，其中包含与*MessageIndex*相对应的新消息。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_SMS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须使用 NDIS\_状态\_WWAN\_SMS\_状态，通知 MB 服务有关所有非类0（闪存/警报）消息的到达。 若要向 MB 服务通知类0（闪存/警报）消息到达，微型端口驱动程序必须使用[**NDIS\_状态\_WWAN\_SMS\_接收**](ndis-status-wwan-sms-receive.md)。

此指示可能是\_WWAN\_SMS\_状态或未经请求的事件的 OID*查询*请求的事务通知。

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


[**NDIS\_WWAN\_SMS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)

[ **\_WWAN\_SMS\_接收的 NDIS\_状态**](ndis-status-wwan-sms-receive.md)

 

 




