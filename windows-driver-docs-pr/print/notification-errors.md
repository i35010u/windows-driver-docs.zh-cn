---
title: 通知错误
description: 通知错误
ms.assetid: ffead40c-5c1c-45f6-83d2-48e4af357255
keywords:
- 后台处理程序通知 WDK 打印，错误
- 打印后台处理程序通知 WDK，错误
- 通知错误 WDK 打印后台处理程序
- 错误 WDK 后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a399cfaab9c784039d247ce98b1135d1ca9e195
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523023"
---
# <a name="notification-errors"></a>通知错误





成员**PrintAsyncNotifyError**枚举的类型用于表示发生错误的类型。 下表描述了可能的错误代码。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>错误代码</th>
<th>值</th>
<th>通信类型</th>
<th>适用于</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CHANNEL_CLOSED_BY_SERVER</p></td>
<td><p>0x01</p></td>
<td></td>
<td></td>
<td><p><strong>SendNotification</strong>并<strong>CloseChannel</strong>打印后台处理程序关闭之前调用通道时返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_CLOSED_BY_ANOTHER_LISTENER</p></td>
<td><p>0x02</p></td>
<td><p>双向</p></td>
<td><p>Listener</p></td>
<td><p>SendNotification 并<strong>CloseChannel</strong>另一个侦听器关闭通道之前调用时返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_CLOSED_BY_SAME_LISTENER</p></td>
<td><p>0x03</p></td>
<td><p>双向</p></td>
<td><p>发件人</p></td>
<td><p><strong>CloseChannel</strong>同一个侦听器关闭通道之前调用时返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_RELEASED_BY_LISTENER</p></td>
<td><p>0x04</p></td>
<td></td>
<td></td>
<td><p><strong>SendNotification</strong>并<strong>CloseChannel</strong>另一个侦听器发布在调用前先通道时返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>UNIRECTIONAL_NOTIFICATION_LOST</p></td>
<td><p>0x05</p></td>
<td><p>单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>一个或多个存在侦听器未收到通知时此值返回给发件人。 发件人发送通知超过了侦听器可以处理更快地时会发生该错误。</p></td>
</tr>
<tr class="even">
<td><p>ASYNC_NOTIFICATION_FAILURE</p></td>
<td><p>0x06</p></td>
<td><p>单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>无存在侦听器接收通知时此值返回给发件人。 这种情况下会在一些有限的系统资源条件...</p></td>
</tr>
<tr class="odd">
<td><p>NO_LISTENERS</p></td>
<td><p>0x07</p></td>
<td><p>单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>作为非错误以指示没有侦听器已注册到发件人返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_ALREADY_CLOSED</p></td>
<td><p>0x08</p></td>
<td><p>双向</p></td>
<td><p>发送方和侦听器</p></td>
<td><p><strong>SendNotification</strong>通道已关闭时返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_ALREADY_OPENED</p></td>
<td><p>0x09</p></td>
<td><p>双向和单向</p></td>
<td><p>发送方和侦听器</p></td>
<td><p><strong>CreateNotificationChannel</strong>通道已打开时，返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_WAITING_FOR_CLIENT_NOTIFICATION</p></td>
<td><p>0x0a</p></td>
<td><p>双向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>通道正在等待客户端通知时，返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_NOT_OPENED</p></td>
<td><p>0x0b</p></td>
<td><p>双向和单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>CreateNotificationChannel</strong>不打开通道时，返回此值。</p></td>
</tr>
<tr class="even">
<td><p>ASYNC_CALL_ALREADY_PARKED</p></td>
<td><p>0x0c</p></td>
<td><p>双向和单向</p></td>
<td><p></p>
发件人 （内部）</td>
<td><p>已在此通道上发起呼叫。 不允许多个调用每个通道一次。</p></td>
</tr>
<tr class="odd">
<td><p>NOT_REGISTERED</p></td>
<td><p>0x0d</p></td>
<td></td>
<td></td>
<td><p><strong>UnregisterForNotifications</strong>尚未注册注册对象时，返回此值。</p></td>
</tr>
<tr class="even">
<td><p>ALREADY_UNREGISTERED</p></td>
<td><p>0x0e</p></td>
<td><p>双向和单向</p></td>
<td><p>Listener</p></td>
<td><p><strong>UnregisterForNotifications</strong>注册对象已注销时，返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>ALREADY_REGISTERED</p></td>
<td><p>0x0f</p></td>
<td><p>双向和单向</p></td>
<td><p>Listener</p></td>
<td><p><strong>RegisterForNotifications</strong>时已注册的注册对象，返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_ACQUIRED</p></td>
<td><p>0x10</p></td>
<td><p>双向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>并<strong>CloseChannel</strong>当另一个侦听器获取通道会返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>ASYNC_CALL_IN_PROGRESS</p></td>
<td><p>0x11</p></td>
<td><p>双向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>调用正在进行时，返回此值。 只有一个调用每个通道允许一次。</p></td>
</tr>
<tr class="even">
<td><p>MAX_NOTIFICATION_SIZE_EXCEEDED</p></td>
<td><p>0x12</p></td>
<td><p>双向和单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>通知数据大小超过允许的最大时返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>INTERNAL_NOTIFICATION_QUEUE_IS_FULL</p></td>
<td><p>0x13</p></td>
<td><p>双向和单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>OnEventNotify</strong>通知队列已满时，返回此值。</p></td>
</tr>
<tr class="even">
<td><p>INVALID_NOTIFICATION_TYPE</p></td>
<td><p>0x14</p></td>
<td><p>双向和单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>SendNotification</strong>则返回此值时通知&#39;s 类型是不同于通道&#39;的类型。</p></td>
</tr>
<tr class="odd">
<td><p>MAX_REGISTRATION_COUNT_EXCEEDED</p></td>
<td><p>0x15</p></td>
<td><p>双向和单向</p></td>
<td><p>Listener</p></td>
<td><p><strong>RegisterForNotifications</strong>注册数超出了允许的最大数目时，返回此值。</p></td>
</tr>
<tr class="even">
<td><p>MAX_CHANNEL_COUNT_EXCEEDED</p></td>
<td><p>0x16</p></td>
<td><p>双向和单向</p></td>
<td><p>发件人</p></td>
<td><p><strong>CreatePrintNotificationChannel</strong>的通道数超出了允许的最大数目时，返回此值。</p></td>
</tr>
</tbody>
</table>

 

 

 




