---
title: NDIS_STATUS_WWAN_SMS_RECEIVE
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_RECEIVE 通知来通知 MB 服务：已通过 OID_WWAN_SMS_READ \ 160; 个查询请求完成了上一个读取请求，或从该请求的作为事件通知的网络提供程序。 小型端口驱动程序还可以通过此通知发送未经请求的事件。此通知使用 NDIS_WWAN_SMS_RECEIVE 结构。
ms.assetid: fc1c3587-8bba-4ffd-9561-4140c307c705
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_WWAN_SMS_RECEIVE 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5bef42d6826fe96369f866fdcff38bcc6c9f2f6f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844636"
---
# <a name="ndis_status_wwan_sms_receive"></a>\_WWAN\_SMS\_接收的 NDIS\_状态


小型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_接收通知，通过[OID\_wwan\_SMS\_读取](oid-wwan-sms-read.md)通知 MB 服务_ 查询请求，或者到达来自网络提供程序的新的类0（闪存/警报）消息作为事件通知。

小型端口驱动程序还可以通过此通知发送未经请求的事件。

此通知使用[**NDIS\_WWAN\_SMS\_接收**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)结构。

<a name="remarks"></a>备注
-------

通过微型端口驱动程序将 RequestId 设置为 "0"，以指示新的类0（闪存/警报）消息到达。 新的类0（闪存/警报）消息到达时，会依赖于当前的网络注册状态。

如果读取请求导致检索无法在微型端口驱动程序的预分配缓冲区中容纳的大量 SMS 记录，则可以在多个指示中将 SMS 记录发送到 MB 服务。 在这种情况下，uStatus 必须设置为 WWAN\_状态\_SMS\_用于中间事务的更\_数据，最终事务必须以 WWAN\_状态\_成功结束。

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

## <a name="see-also"></a>另请参阅


[OID\_WWAN\_SMS\_读取](oid-wwan-sms-read.md)

[**NDIS\_WWAN\_SMS\_接收**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_sms_receive)

 

 




