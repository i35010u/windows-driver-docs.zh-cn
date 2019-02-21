---
title: Bug 检查 0x14F PDC_WATCHDOG_TIMEOUT
description: PDC_WATCHDOG_TIMEOUT bug 检查具有 0x0000014F 值。 这表示系统组件未能在分配的时间段内响应。
ms.assetid: 347D31C2-7027-44BD-A0E8-60C6EC3A2030
keywords:
- Bug 检查 0x14F PDC_WATCHDOG_TIMEOUT
- PDC_WATCHDOG_TIMEOUT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PDC_WATCHDOG_TIMEOUT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 941462301b38d26d462e5d51d320316cd50bee22
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546517"
---
# <a name="bug-check-0x14f-pdcwatchdogtimeout"></a>Bug 检查 0x14F:PDC\_监视器\_超时


PDC\_监视器\_超时错误检查的值为 0x0000014F。 这表示无法阻止退出系统分配的时间内响应的系统组件连接待机。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="pdcwatchdogtimeout-parameters"></a>PDC\_监视器\_超时参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">1</td>
<td align="left">挂起的组件的客户端 ID。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>挂起的组件的客户端类型。</p>
<p>0x1:通知客户端未能响应。</p>
参数 3:指向通知客户端 (PDC_NOTIFICATION_CLIENT)。
参数 4:指向 pdc ！PDC_14F_TRIAGE 结构。
<p>0x2:弹性客户端未能响应。</p>
参数 3:弹性客户端 (PDC_RESILIENCY_CLIENT) 的指针。
参数 4:指向 pdc ！PDC_14F_TRIAGE 结构。
<p>0x3:激活器客户端保留的时间太长的引用。</p>
参数 3:指向激活客户端 (pdc ！ _PDC_ACTIVATOR_CLIENT)。
参数 4:指向 pdc ！PDC_14F_TRIAGE 结构。
<p>0x100:Win32k 未及时完成一个监视器上的请求。</p>
参数 3:此请求的最新的 POWER_MONITOR_REQUEST_REASON 值。
参数 4:一个值，该值以发起该请求所采用的内部路径。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 2</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 2</td>
</tr>
</tbody>
</table>


## <a name="resolution"></a>分辨率

[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。
 

 

 




