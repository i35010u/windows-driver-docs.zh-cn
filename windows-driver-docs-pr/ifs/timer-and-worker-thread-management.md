---
title: 计时器和工作线程管理
description: 计时器和工作线程管理
ms.assetid: b1feeb4a-0555-4ed6-a26c-ef2a5fc58280
keywords:
- RDBSS WDK 文件系统中，辅助角色线程管理
- 重定向驱动器缓冲子系统 WDK 文件系统中，辅助角色线程管理
- RDBSS WDK 文件系统中计时器
- 重定向驱动器缓冲子系统 WDK 文件系统中计时器
- 计时器 WDK RDBSS
- 工作线程数 WDK RDBSS
- 单步通知 WDK RDBSS
- 定期触发器 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19452c73b5791200316e6ab67e3736fa2ddfc523
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380329"
---
# <a name="timer-and-worker-thread-management"></a>计时器和工作线程管理


## <span id="ddk_timer_and_worker_thread_management_if"></span><span id="DDK_TIMER_AND_WORKER_THREAD_MANAGEMENT_IF"></span>


RDBSS 提供辅助角色线程管理多个计时器例程。 这些服务提供给所有网络微型重定向程序驱动程序。 提供了以下类型的计时器例程：

-   定期触发器

-   单步通知

计时器是与设备对象和一个辅助角色线程例程相关联。 当计时器到期时，辅助角色线程例程作为输入参数传递到初始**RxPostOneShotTimerRequest**或**RxPostRecurrentTimerRequest**调用例程。

包含以下 RDBSS 计时器例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxcanceltimerrequest" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxcanceltimerrequest)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>此例程会取消计时器请求。 要取消该请求由指向该例程和上下文参数的标识。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostoneshottimerrequest" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostoneshottimerrequest)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>驱动程序使用此例程来初始化一次性计时器请求。 传递给此例程的辅助角色线程例程后计时器过期时调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>此例程初始化循环计时器请求。 辅助角色线程例程，传递给此例程称为按固定间隔重复的计时器将激发时基于此例程的输入参数。</p></td>
</tr>
</tbody>
</table>

 

 

 




