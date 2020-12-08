---
title: 通知错误
description: 通知错误
keywords:
- 后台处理程序通知 WDK 打印，错误
- 打印后台处理程序通知 WDK，错误
- 通知错误 WDK 打印后台处理程序
- 错误 WDK 后台处理程序通知
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ace27b15d8230c6c709524f9a4e780db00f262a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807767"
---
# <a name="notification-errors"></a>通知错误





**PrintAsyncNotifyError** 枚举类型的成员用于表示发生的错误的类型。 下表描述了可能的错误代码。

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
<th>“值”</th>
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
<td><p>当打印后台处理程序在调用之前关闭频道时， <strong>SendNotification</strong>和<strong>CloseChannel</strong>返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_CLOSED_BY_ANOTHER_LISTENER</p></td>
<td><p>0x02</p></td>
<td><p>双向</p></td>
<td><p>侦听器</p></td>
<td><p>当另一个侦听器在调用之前关闭信道时，SendNotification 和 <strong>CloseChannel</strong> 将返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_CLOSED_BY_SAME_LISTENER</p></td>
<td><p>0x03</p></td>
<td><p>双向</p></td>
<td><p>发送方</p></td>
<td><p>当同一侦听器在调用之前关闭通道时， <strong>CloseChannel</strong>将返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_RELEASED_BY_LISTENER</p></td>
<td><p>0x04</p></td>
<td></td>
<td></td>
<td><p>当另一个侦听器在调用之前释放通道时， <strong>SendNotification</strong>和<strong>CloseChannel</strong>将返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>UNIRECTIONAL_NOTIFICATION_LOST</p></td>
<td><p>0x05</p></td>
<td><p>单向</p></td>
<td><p>发送方</p></td>
<td><p>当一个或多个现有侦听器未收到通知时， <strong>SendNotification</strong>会将此值返回给发件人。 如果发送方发送通知的速度比侦听器可以处理的速度快，则会发生这种情况。</p></td>
</tr>
<tr class="even">
<td><p>ASYNC_NOTIFICATION_FAILURE</p></td>
<td><p>0x06</p></td>
<td><p>单向</p></td>
<td><p>发送方</p></td>
<td><p>当当前没有侦听器收到通知时， <strong>SendNotification</strong>会将此值返回给发件人。 这种情况可能会在有限的系统资源条件下出现。</p></td>
</tr>
<tr class="odd">
<td><p>NO_LISTENERS</p></td>
<td><p>0x07</p></td>
<td><p>单向</p></td>
<td><p>发送方</p></td>
<td><p><strong>SendNotification</strong> 将此值作为非错误返回给发件人，以指示没有注册侦听器。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_ALREADY_CLOSED</p></td>
<td><p>0x08</p></td>
<td><p>双向</p></td>
<td><p>发送方和侦听器</p></td>
<td><p>当频道已关闭时， <strong>SendNotification</strong>将返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_ALREADY_OPENED</p></td>
<td><p>0x09</p></td>
<td><p>双向和单向</p></td>
<td><p>发送方和侦听器</p></td>
<td><p>当频道已打开时， <strong>CreateNotificationChannel</strong>将返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_WAITING_FOR_CLIENT_NOTIFICATION</p></td>
<td><p>0x0a</p></td>
<td><p>双向</p></td>
<td><p>发送方</p></td>
<td><p>当通道正在等待客户端通知时， <strong>SendNotification</strong>将返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>CHANNEL_NOT_OPENED</p></td>
<td><p>0x0b</p></td>
<td><p>双向和单向</p></td>
<td><p>发送方</p></td>
<td><p>当通道尚未打开时， <strong>CreateNotificationChannel</strong>将返回此值。</p></td>
</tr>
<tr class="even">
<td><p>ASYNC_CALL_ALREADY_PARKED</p></td>
<td><p>0x0c</p></td>
<td><p>双向和单向</p></td>
<td><p></p>
发件人 (内部) </td>
<td><p>已在此通道上发出调用。 不允许每个通道一次调用多个。</p></td>
</tr>
<tr class="odd">
<td><p>NOT_REGISTERED</p></td>
<td><p>0x0d</p></td>
<td></td>
<td></td>
<td><p>当注册对象尚未注册时， <strong>UnregisterForNotifications</strong>将返回此值。</p></td>
</tr>
<tr class="even">
<td><p>ALREADY_UNREGISTERED</p></td>
<td><p>0x0e</p></td>
<td><p>双向和单向</p></td>
<td><p>侦听器</p></td>
<td><p>注册对象已取消注册后， <strong>UnregisterForNotifications</strong>将返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>ALREADY_REGISTERED</p></td>
<td><p>0x0f</p></td>
<td><p>双向和单向</p></td>
<td><p>侦听器</p></td>
<td><p>当注册对象已注册时， <strong>RegisterForNotifications</strong>将返回此值。</p></td>
</tr>
<tr class="even">
<td><p>CHANNEL_ACQUIRED</p></td>
<td><p>0x10</p></td>
<td><p>双向</p></td>
<td><p>发送方</p></td>
<td><p>当另一个侦听器获取通道时， <strong>SendNotification</strong>和<strong>CloseChannel</strong>返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>ASYNC_CALL_IN_PROGRESS</p></td>
<td><p>0x11</p></td>
<td><p>双向</p></td>
<td><p>发送方</p></td>
<td><p>当调用已在进行时， <strong>SendNotification</strong>返回此值。 一次只允许对每个通道进行一次调用。</p></td>
</tr>
<tr class="even">
<td><p>MAX_NOTIFICATION_SIZE_EXCEEDED</p></td>
<td><p>0x12</p></td>
<td><p>双向和单向</p></td>
<td><p>发送方</p></td>
<td><p>当通知数据的大小超过允许的最大值时， <strong>SendNotification</strong>将返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>INTERNAL_NOTIFICATION_QUEUE_IS_FULL</p></td>
<td><p>0x13</p></td>
<td><p>双向和单向</p></td>
<td><p>发送方</p></td>
<td><p>当通知队列已满时， <strong>OnEventNotify</strong>将返回此值。</p></td>
</tr>
<tr class="even">
<td><p>INVALID_NOTIFICATION_TYPE</p></td>
<td><p>0x14</p></td>
<td><p>双向和单向</p></td>
<td><p>发送方</p></td>
<td><p>当通知的类型不同于通道的类型时， <strong>SendNotification</strong>将返回此值。</p></td>
</tr>
<tr class="odd">
<td><p>MAX_REGISTRATION_COUNT_EXCEEDED</p></td>
<td><p>0x15</p></td>
<td><p>双向和单向</p></td>
<td><p>侦听器</p></td>
<td><p>当注册数量超过了允许的最大数目时， <strong>RegisterForNotifications</strong>将返回此值。</p></td>
</tr>
<tr class="even">
<td><p>MAX_CHANNEL_COUNT_EXCEEDED</p></td>
<td><p>0x16</p></td>
<td><p>双向和单向</p></td>
<td><p>发送方</p></td>
<td><p>当通道数超出允许的最大数目时， <strong>CreatePrintNotificationChannel</strong>将返回此值。</p></td>
</tr>
</tbody>
</table>

 

 

 




