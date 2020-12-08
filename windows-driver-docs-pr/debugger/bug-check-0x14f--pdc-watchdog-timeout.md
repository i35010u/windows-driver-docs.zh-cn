---
title: Bug 检查 0x14F PDC_WATCHDOG_TIMEOUT
description: PDC_WATCHDOG_TIMEOUT bug 检查的值为0x0000014F。 这表明系统组件未能在分配的时间段内响应。
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
ms.openlocfilehash: 2c0194c8fdcdf6ae366de61d1811546102f13f27
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790699"
---
# <a name="bug-check-0x14f-pdc_watchdog_timeout"></a>Bug 检查0x14F： PDC \_ 监视程序 \_ 超时


PDC \_ 监视程序 \_ 超时 bug 检查的值为0x0000014F。 这表明系统组件未能在分配的时间段内响应，从而阻止系统退出连接待机状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="pdc_watchdog_timeout-parameters"></a>PDC \_ 监视程序 \_ 超时参数


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
<td align="left">挂起组件的客户端 ID。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left"><p>挂起组件的客户端类型。</p>
<p>0x1：通知客户端未能响应。</p>
参数3：指向通知客户端 (PDC_NOTIFICATION_CLIENT) 的指针。
参数4：指向 pdc！PDC_14F_TRIAGE 结构。
<p>0x2：复原客户端未能响应。</p>
参数3：指向复原客户端的指针 (PDC_RESILIENCY_CLIENT) 。
参数4：指向 pdc！PDC_14F_TRIAGE 结构。
<p>0x3：激活器客户端持有引用的时间太长。</p>
参数3：指向激活客户端 (pdc！ _PDC_ACTIVATOR_CLIENT) 的指针。
参数4：指向 pdc！PDC_14F_TRIAGE 结构。
<p>0x100： Win32k.sys 未及时完成监视器上的请求。</p>
参数3：此请求的最新 POWER_MONITOR_REQUEST_REASON 值。
参数4：指示启动请求所需的内部路径的值。</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数2</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数2</td>
</tr>
</tbody>
</table>


## <a name="resolution"></a>解决方法

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
 

 

 




