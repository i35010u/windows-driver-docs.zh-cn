---
title: NDIS_STATUS_WWAN_SMS_STATUS
description: 微型端口驱动程序使用 NDIS_STATUS_WWAN_SMS_STATUS 通知以下事件的 MB 设备的消息存储情况通知给 MB 服务已满。新的 SMS 文本消息已到达，对应于 MessageIndex.Miniport 的新消息与驱动程序还可以发送未经请求的事件与该通知。此通知使用 NDIS_WWAN_SMS_STATUS 结构。
ms.assetid: 65553a3f-57af-49ef-a3b7-ed35df0a319d
ms.date: 08/08/2017
keywords: -NDIS_STATUS_WWAN_SMS_STATUS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: c60af8cff49121851565aa71b41cd1eb8dcb20e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372215"
---
# <a name="ndisstatuswwansmsstatus"></a>NDIS\_状态\_WWAN\_SMS\_状态


微型端口驱动程序使用 NDIS\_状态\_WWAN\_SMS\_状态通知来通知 MB 服务有关的以下事件：

-   MB 设备的消息存储区已满。

-   已接收到新的 SMS 文本消息，使用新消息相对应的*MessageIndex*。

微型端口驱动程序还可以发送未经请求的事件与该通知。

使用此通知[ **NDIS\_WWAN\_SMS\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567945)结构。

<a name="remarks"></a>备注
-------

微型端口驱动程序必须使用 NDIS\_状态\_WWAN\_SMS\_状态以告知 MB 服务有关的所有非类-0 （flash/警报） 消息到达。 若要告知类 0 （flash/警报） 消息到达 MB 服务，微型端口驱动程序必须使用[ **NDIS\_状态\_WWAN\_SMS\_接收**](ndis-status-wwan-sms-receive.md).

此指示可能的事务通知*查询*OID 请求\_WWAN\_SMS\_状态或未经请求的事件。

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


[**NDIS\_WWAN\_SMS\_STATUS**](https://msdn.microsoft.com/library/windows/hardware/ff567945)

[**NDIS\_STATUS\_WWAN\_SMS\_RECEIVE**](ndis-status-wwan-sms-receive.md)

 

 




