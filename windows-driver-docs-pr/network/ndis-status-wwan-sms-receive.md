---
title: NDIS_STATUS_WWAN_SMS_RECEIVE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_RECEIVE 通知，通过 OID_WWAN_SMS_READ \ 160; 查询请求或从网络提供程序到新的类-0 (闪存/警报) 消息来通知 MB 服务是否已完成。 小型端口驱动程序还可以通过此通知发送未经请求的事件。此通知使用 NDIS_WWAN_SMS_RECEIVE 结构。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_RECEIVE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 034323526a75961765cfe36b2b9077159d225eff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837933"
---
# <a name="ndis_status_wwan_sms_receive"></a>NDIS \_ 状态 \_ WWAN \_ SMS \_ 接收


微型端口驱动程序使用 NDIS \_ 状态 " \_ wwan \_ sms 接收通知"， \_ 通过 [OID \_ WWAN \_ sms \_ 读取](oid-wwan-sms-read.md) 查询请求通知 MB 服务，或从网络提供商处到达新的类 0 (闪存/警报) 消息作为事件通知。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用 [**NDIS \_ WWAN \_ SMS \_ 接收**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive) 结构。

<a name="remarks"></a>备注
-------

使用端口驱动程序将 RequestId 设置为 "0"，以指示新类的到达-0 (flash/alert) 消息。 新的类 0 (闪存/警报) 消息依赖于当前网络注册状态。

如果读取请求导致检索无法在微型端口驱动程序的预分配缓冲区中容纳的大量 SMS 记录，则可以在多个指示中将 SMS 记录发送到 MB 服务。 在这种情况下，必须将 uStatus 设置为 WWAN \_ 状态 \_ SMS \_ 更多 \_ 的中间事务数据，最终事务必须以 wwan \_ 状态 "成功" 结束 \_ 。

下图显示了多个指示方法对大量 SMS 记录检索的用法：

![说明多个指示方法对大量 sms 记录检索的使用情况的关系图](images/wwansmsrecordretrieval.png)

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


[OID \_ WWAN \_ SMS \_ 读取](oid-wwan-sms-read.md)

[**NDIS \_ WWAN \_ SMS \_ 接收**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)

 

