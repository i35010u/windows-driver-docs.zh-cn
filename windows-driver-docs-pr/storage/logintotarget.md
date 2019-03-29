---
title: LoginToTarget
description: LoginToTarget
ms.assetid: 9ad66387-ca77-46e7-aa91-5c909251c2ce
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 483566fd2e5a7310b6147bfa3899c928aeaf8d02
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575676"
---
# <a name="logintotarget"></a>LoginToTarget


**LoginToTarget**方法指示管理 HBA 发起程序登录到目标门户的微型端口驱动程序。

实现的微型端口驱动程序[MSiSCSI\_Operations WMI 类](msiscsi-operations-wmi-class.md)必须支持此方法。

微型端口驱动程序必须公开有关它通过创建会话的信息[MSiSCSI\_InitiatorSessionInfo WMI 类](msiscsi-initiatorsessioninfo-wmi-class.md)。

下表介绍的发起程序可以建立登录会话的类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">登录会话</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>发现</p></td>
<td align="left"><p>发现讨论会专门用于<strong>SendTargets</strong>操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>信息性</p></td>
<td align="left"><p>信息性会话允许发起程序可以查询的目标的信息，但发起方不会报告给插 (PnP) 管理器; 在目标上的逻辑单元号 (Lun)存储端口驱动程序不会枚举这些 Lun 或将它们公开为本地设备。 管理应用程序可以通过建立的信息性会话并调用 iSCSI 用户模式库例程，如查询这些远程 Lun <strong>SendScsiInquiry</strong>， <strong>SendScsiReportLuns</strong>，和<strong>SendScsiReadCapacity</strong>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据</p></td>
<td align="left"><p>数据会话是全功能的会话。 启动会话的微型端口驱动程序报告 Lun 的目标上端口驱动程序，因此端口驱动程序将枚举它们并加载相应的驱动程序。 软件可以访问这些远程设备，就像它们是本地的设备。</p></td>
</tr>
<tr class="even">
<td align="left"><p>启动</p></td>
<td align="left"><p>启动会话是全功能的会话的 iSCSI LUN 用作启动设备。</p></td>
</tr>
</tbody>
</table>

 

标识符 (ID) 的**LoginToTarget**方法分配到该会话必须保持不变的会话生存期内。 即使异步注销或网络事件断开连接到目标，并强制微型端口驱动程序重新连接，微型端口驱动程序应继续使用相同的会话 id。

当他们重新建立数据和信息性会话时，微型端口驱动程序应使用以下准则：

<span id="Periodic_reconnection_attempts"></span><span id="periodic_reconnection_attempts"></span><span id="PERIODIC_RECONNECTION_ATTEMPTS"></span>定期重新连接尝试  
微型端口驱动程序应进行定期尝试重新连接 （建议使用间隔为 5 秒） 之前进行的登录操作是成功还是微型端口驱动程序收到的注销请求。

<span id="Device_removal_latency"></span><span id="device_removal_latency"></span><span id="DEVICE_REMOVAL_LATENCY"></span>设备删除延迟  
微型端口驱动程序不应立即删除目标的逻辑单元从本地操作系统的设备堆栈。 相反，微型端口驱动程序应使用处理查询和报表 LUN 请求和队列请求微型端口驱动程序必须处理发送到远程目标的本地缓存的数据。

如果无法在大约 60 秒之后重新建立与目标会话微型端口驱动程序，它应从本地设备堆栈中移除目标的逻辑单元。 通过引入从设备堆栈中的设备删除 60 秒的延迟，微型端口驱动程序可以避免不必要地中断远程目标上的数据访问的本地应用程序的工作。 但是，超过 60 秒的延迟，可能需要进行排队的请求，过多的微型端口驱动程序，这些请求可能会消耗大量系统资源。 确切的滞后时间应为可配置。

**LoginToTarget** WMI 方法属于[MSiSCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)。

有关 iSCSI 用户模式下库用来建立日志的算法的说明，请参阅**LoginIScsiTarget**。

 

 





