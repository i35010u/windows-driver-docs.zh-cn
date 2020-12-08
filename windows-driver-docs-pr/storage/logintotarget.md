---
title: LoginToTarget
description: LoginToTarget
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bfbbddd5b5386937ab5b614e75ae2a743d46930f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811603"
---
# <a name="logintotarget"></a>LoginToTarget


**LoginToTarget** 方法指示一个小型端口驱动程序，该驱动程序管理 HBA 发起程序以登录到目标门户。

实现 [MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md) 的微型端口驱动程序必须支持此方法。

微型端口驱动程序必须公开有关通过 [MSiSCSI \_ InitiatorSessionInfo WMI 类](msiscsi-initiatorsessioninfo-wmi-class.md)创建的会话的信息。

下表描述了发起程序可以建立的登录会话的类型。

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
<td align="left"><p>发现会话仅用于 <strong>SendTargets</strong> 操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p>信息</p></td>
<td align="left"><p>信息会话允许发起方在目标中查询信息，但发起方不会将目标 (Lun) 的逻辑单元号报告到即插即用 (PnP) 管理器;存储端口驱动程序不会枚举 Lun，也不会将它们公开为本地设备。 管理应用程序可以通过建立信息性会话和调用 iSCSI 用户模式库例程（如 <strong>SendScsiInquiry</strong>、 <strong>SendScsiReportLuns</strong>和 <strong>SendScsiReadCapacity</strong>）来查询这些远程 lun。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>数据</p></td>
<td align="left"><p>数据会话是功能完备的会话。 启动会话的微型端口驱动程序应向端口驱动程序报告目标上的 Lun，因此端口驱动程序将枚举它们并加载相应的驱动程序。 软件可以访问这些远程设备，就好像它们是本地设备一样。</p></td>
</tr>
<tr class="even">
<td align="left"><p>启动</p></td>
<td align="left"><p>启动会话是一个功能完备的会话，在该会话中，iSCSI LUN 用作启动设备。</p></td>
</tr>
</tbody>
</table>

 

**LoginToTarget** 方法分配给会话的标识符 (ID) 在会话的生存期内必须保持不变。 即使异步注销或网络事件会断开与目标的连接，并强制重新连接微型端口驱动程序，微型端口驱动程序也应继续使用相同的会话 ID。

小型端口驱动程序在重新建立数据和信息性会话时应使用以下准则：

<span id="Periodic_reconnection_attempts"></span><span id="periodic_reconnection_attempts"></span><span id="PERIODIC_RECONNECTION_ATTEMPTS"></span>定期重新连接尝试  
如果登录成功，或微型端口驱动程序收到注销请求，微型端口驱动程序应定期尝试重新连接 (5 秒的时间) 间隔。

<span id="Device_removal_latency"></span><span id="device_removal_latency"></span><span id="DEVICE_REMOVAL_LATENCY"></span>设备删除延迟  
小型端口驱动程序不应立即从本地操作系统的设备堆栈中删除目标的逻辑单元。 相反，微型端口驱动程序应使用本地缓存的数据来处理查询和报表 LUN 请求，并将微型端口驱动程序必须发送到远程目标的请求排队以进行处理。

如果微型端口驱动程序在大约60秒后无法重新建立与目标的会话，它应从本地设备堆栈中删除目标的逻辑单元。 通过引入从设备堆栈中删除设备的60秒延迟，微型端口驱动程序可以避免不必要地中断访问远程目标上数据的本地应用程序的工作。 不过，延迟超过60秒可能要求微型端口驱动程序对大量的请求进行排队，并且这些请求可能会消耗不可接受的系统资源量。 确切的延迟时间应该是可配置的。

**LoginToTarget** wmi 方法属于 [MSiSCSI \_ 操作 wmi 类](msiscsi-operations-wmi-class.md)。

有关 iSCSI 用户模式库用于建立日志的算法的说明，请参阅 **LoginIScsiTarget**。

 

 





