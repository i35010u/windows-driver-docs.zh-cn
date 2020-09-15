---
title: 计时器和工作线程管理
description: 计时器和工作线程管理
ms.assetid: b1feeb4a-0555-4ed6-a26c-ef2a5fc58280
keywords:
- RDBSS WDK 文件系统，工作线程管理
- 重定向驱动器缓冲子系统 WDK 文件系统、工作线程管理
- RDBSS WDK 文件系统，计时器
- 重定向驱动器缓冲子系统 WDK 文件系统、计时器
- 计时器 WDK RDBSS
- 工作线程 WDK RDBSS
- 一次性通知 WDK RDBSS
- 定期触发 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2dc17d1fbdf84a200ded866527066602c900acd8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107170"
---
# <a name="timer-and-worker-thread-management"></a>计时器和工作线程管理


## <span id="ddk_timer_and_worker_thread_management_if"></span><span id="DDK_TIMER_AND_WORKER_THREAD_MANAGEMENT_IF"></span>


RDBSS 为工作线程管理提供了多个计时器例程。 这些服务是为所有网络最小化的驱动程序驱动程序提供的。 提供以下类型的计时器例程：

-   定期触发器

-   一次性通知

计时器与设备对象和工作线程例程相关联。 当计时器过期时，将调用作为输入参数传递到初始 **RxPostOneShotTimerRequest** 或 **RxPostRecurrentTimerRequest** 例程的工作线程例程。

包含以下 RDBSS 计时器例程。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">例程所返回的值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest" data-raw-source="[&lt;strong&gt;RxCancelTimerRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxcanceltimerrequest)"><strong>RxCancelTimerRequest</strong></a></p></td>
<td align="left"><p>此例程取消计时器请求。 要取消的请求由指向例程和上下文参数的指针标识。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest" data-raw-source="[&lt;strong&gt;RxPostOneShotTimerRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostoneshottimerrequest)"><strong>RxPostOneShotTimerRequest</strong></a></p></td>
<td align="left"><p>驱动程序使用此例程来初始化一次拍摄计时器请求。 当计时器过期时，传递给此例程的工作线程例程将被调用一次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest" data-raw-source="[&lt;strong&gt;RxPostRecurrentTimerRequest&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxtimer/nf-rxtimer-rxpostrecurrenttimerrequest)"><strong>RxPostRecurrentTimerRequest</strong></a></p></td>
<td align="left"><p>此例程初始化重复性计时器请求。 当重复性计时器根据此例程的输入参数触发时，传递给此例程的工作线程例程会定期调用。</p></td>
</tr>
</tbody>
</table>

 

