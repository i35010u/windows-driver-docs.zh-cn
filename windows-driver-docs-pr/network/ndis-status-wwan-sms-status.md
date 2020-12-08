---
title: NDIS_STATUS_WWAN_SMS_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_STATUS 通知来通知 MB 服务以下事件 MB 设备的消息存储已满。新的 SMS 文本消息已到达，新消息与 MessageIndex 驱动程序相对应，还可以使用此通知发送未经请求的事件。此通知使用 NDIS_WWAN_SMS_STATUS 结构。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_STATUS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: a38fc2e0478630a78d2a26eda0db2f6f02802f5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809999"
---
# <a name="ndis_status_wwan_sms_status"></a>NDIS \_ 状态 \_ WWAN \_ SMS \_ 状态


微型端口驱动程序使用 NDIS \_ 状态 \_ WWAN \_ SMS \_ 状态通知来通知 MB 服务有关以下事件：

-   MB 设备的消息存储已满。

-   已到达新的短信消息，其中包含与 *MessageIndex* 相对应的新消息。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ SMS \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status) 结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须使用 NDIS \_ 状态 \_ WWAN \_ SMS \_ 状态通知 MB 服务所有非类 (闪存/警报) 消息到达。 若要通知 MB 服务 () 消息到达，微型端口驱动程序必须使用 [**NDIS \_ 状态 \_ WWAN \_ SMS \_ 接收**](ndis-status-wwan-sms-receive.md)。

此指示可以是针对 OID *query* \_ WWAN \_ SMS \_ 状态或未经许可事件的查询请求的事务通知。

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

## <a name="see-also"></a>请参阅


[**NDIS \_ WWAN \_ SMS \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_status)

[**NDIS \_ 状态 \_ WWAN \_ SMS \_ 接收**](ndis-status-wwan-sms-receive.md)

 

