---
title: NDIS_STATUS_WWAN_SMS_RECEIVE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_RECEIVE 通知来告知 OID_WWAN_SMS_READ 通过的上一个读取请求完成 MB 服务 \ 160; 查询请求或从新类 0 （flash/警报） 消息的到达作为事件通知的网络提供程序。 微型端口驱动程序还可以发送未经请求的事件与该通知。此通知使用 NDIS_WWAN_SMS_RECEIVE 结构。
ms.assetid: fc1c3587-8bba-4ffd-9561-4140c307c705
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_RECEIVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 6a96462b0876c17d52c34b5091d64afb9a891e3a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372537"
---
# <a name="ndisstatuswwansmsreceive"></a>NDIS\_状态\_WWAN\_SMS\_接收


微型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_接收通知，以通过的上一个读取请求完成有关通知 MB 服务[OID\_WWAN\_短信\_读取](oid-wwan-sms-read.md) 查询请求或作为事件通知的网络提供程序的新类 0 （flash/警报） 消息到达。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_SMS\_接收**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)结构。

<a name="remarks"></a>备注
-------

请求 Id 设置为"0"的微型端口驱动程序以指示新的类 0 （flash/警报） 消息的到达。 新类 0 （flash/警报） 消息的到达时间是依赖于当前网络注册状态。

如果为请求读取检索中的大量无法容纳微型端口驱动程序的预分配缓冲区中的 SMS 记录的结果，则 SMS 记录可以发送到中多个指示的 MB 服务。 在这种情况下必须为 WWAN 设置 uStatus\_状态\_SMS\_详细\_中间事务和最后一个的事务数据必须结束 WWAN\_状态\_成功。

下图显示大量的 SMS 记录检索多个指示方法的使用情况：

![说明针对的 sms 记录检索大量的多个指示方法的使用情况的关系图](images/wwansmsrecordretrieval.png)

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


[OID\_WWAN\_SMS\_READ](oid-wwan-sms-read.md)

[**NDIS\_WWAN\_SMS\_RECEIVE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)

 

 




