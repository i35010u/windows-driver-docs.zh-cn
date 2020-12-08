---
title: Bug 检查 0x15F CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP
description: CONNECTED_STANDBY_WATCHDOG_TIMEOUT_LIVEDUMP bug 检查的值为0x0000015F。 这表示已连接待机监视器超时。
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
ms.openlocfilehash: 028cafbc6c33cd720ca9d96b1dfb005f29264a6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830785"
---
# <a name="bug-check-0x15f-connected_standby_watchdog_timeout_livedump"></a>Bug 检查0x15F：连接 \_ 备用 \_ 监视器 \_ 超时 \_ LIVEDUMP


连接的 \_ 待机 \_ 监视程序 \_ 超时 \_ LIVEDUMP bug 检查的值为0x0000015F。 这表示已连接待机监视器超时。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="connected_standby_watchdog_timeout_livedump-parameters"></a>连接 \_ 备用 \_ 监视器 \_ 超时 \_ LIVEDUMP 参数


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
<td align="left"><p>CS 监视子代码</p>
0x1： DRIPS 监视程序超时。 系统已处于连接备用的复原阶段，无激活激活，且没有设备约束的时间太长，无需进入 DRIPS (最深的运行时空闲平台状态) 。
<p>2-指向附加信息的指针 (nt！POP_DRIPS_WATCHDOG_METRICS) </p>
<p>3-非 DRIPS 的持续时间（毫秒）</p>
<p>4-保留</p>
0x2： DRIPS 监视程序设备约束超时。 系统处于连接待机状态的复原阶段过长，无需进入 DRIPS (最深的运行时空闲平台状态) ，因为没有处于活动状态的未满足的设备约束。
<p>2-nt！TRIAGE_POP_FX_DEVICE 设备</p>
<p>3-组件索引</p>
<p>4-保留</p>
0x3： DRIPS 监视器 preveto 超时。 系统处于连接待机状态的复原阶段的时间太长，无需进入 DRIPS (最深的运行时空闲平台状态) ，因为没有未满足的设备约束且没有活动的激活程序的活动 PEP 预先否决。
<p>2-否决代码</p>
<p>3-指向否决名称字符串的指针 (PWSTR) </p>
<p>4-指向 PEP PPM 回调的指针</p>
0x4：深度睡眠监视器
<p>2-指标</p>
<p>3-NonDeepSleepDurationMs</p>
<p>4-保留</p>
0x5：深度睡眠电源设置监视器
<p>2-指标</p>
<p>3-NonDeepSleepDurationMs</p>
<p>4-保留</p></td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数1</td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此计算机显示的行为会降低屏幕的电池寿命。 这通常是由 CPU 活动、设备活动或设备处于空闲状态不足引起的。

 

 




