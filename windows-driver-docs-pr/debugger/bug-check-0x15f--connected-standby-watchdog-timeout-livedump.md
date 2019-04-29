---
title: Bug 检查 0x15F CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
description: CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP bug 检查具有 0x0000015F 值。 这指示已发生连接备用监视器超时。
ms.assetid: 4C10AAC1-0B8F-4BBE-B470-55A8ED373687
keywords:
- Bug 检查 0x15F CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
- CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: de9c421a4df43cb048989daedaa5eb046ac21dec
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63358107"
---
# <a name="bug-check-0x15f-connectedstandbywatchdogtimeoutlivedump"></a>Bug 检查 0x15F：连接\_待机\_监视器\_超时\_LIVEDUMP


已连接\_待机\_监视器\_超时\_LIVEDUMP bug 检查的值为 0x0000015F。 这指示已发生连接备用监视器超时。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="connectedstandbywatchdogtimeoutlivedump-parameters"></a>连接\_待机\_监视器\_超时\_LIVEDUMP 参数


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
<td align="left"><p>CS 监视器子代码</p>
0x1:DRIPS 监视程序超时。 该系统已经没有的激活器活动和未满足的任何设备约束与连接待机的复原能力阶段中时间太长而无需输入 DRIPS （最深的运行时空闲平台状态）。
<p>2-一个指向其他信息 (nt ！POP_DRIPS_WATCHDOG_METRICS)</p>
<p>3-非 DRIPS 持续时间以毫秒为单位</p>
<p>4-保留</p>
0x2:DRIPS 监视程序设备约束超时。 该系统已经在用于连接待机复原阶段时间太长而无需输入 DRIPS （最深的运行时空闲平台状态） 与活动没有激活器的未满足的设备限制引起的。
<p>2-nt ！TRIAGE_POP_FX_DEVICE 设备</p>
<p>3-组件索引</p>
<p>4-保留</p>
0x3:DRIPS 监视程序 preveto 超时。 该系统已经在用于连接待机复原阶段时间太长而无需输入 DRIPS （最深的运行时空闲平台状态） 由于 active PEP 预否决权没有未满足的设备约束以及活动没有激活器。
<p>2-否决权代码</p>
<p>3-一个指向否决权名称字符串 (PWSTR)</p>
<p>4-一个指向 PEP PPM 回调</p>
0x4:沉睡状态监视器
<p>2-指标</p>
<p>3 -NonDeepSleepDurationMs</p>
<p>4-保留</p>
0x5:深度睡眠电源设置监视器
<p>2-指标</p>
<p>3 -NonDeepSleepDurationMs</p>
<p>4-保留</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 1</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此计算机暴露行为，从而减少屏幕关闭电池寿命。 通常这被由于 CPU 活动、 设备活动或没有足够的空闲状态的设备。

 

 




