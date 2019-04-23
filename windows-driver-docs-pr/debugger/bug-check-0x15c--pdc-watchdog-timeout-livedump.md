---
title: Bug 检查 0x15C PDC_WATCHDOG_TIMEOUT_LIVEDUMP
description: PDC_WATCHDOG_TIMEOUT_LIVEDUMP bug 检查阻止进入或退出连接的待机 0x0000015C，指示无法响应，系统组件的值。
ms.assetid: 4FBB884D-99B5-4564-95D5-396323651C5A
keywords:
- Bug 检查 0x15C PDC_WATCHDOG_TIMEOUT_LIVEDUMP
- PDC_WATCHDOG_TIMEOUT_LIVEDUMP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PDC_WATCHDOG_TIMEOUT_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5d8452e308dad73bb3c99d57224302a1623be8cb
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903959"
---
# <a name="bug-check-0x15c-pdcwatchdogtimeoutlivedump"></a>Bug 检查 0x15C：PDC\_监视器\_超时\_LIVEDUMP


PDC\_监视器\_超时\_LIVEDUMP bug 检查的值为 0x0000015C。 这表示系统组件无法阻止从进入或退出连接的待机系统分配的时间内响应。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="pdcwatchdogtimeoutlivedump-parameters"></a>PDC\_监视器\_超时\_LIVEDUMP 参数


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
0x1:通知客户端未能响应。
<p>3-指针，指向通知客户端 (pdc ！ _PDC_NOTIFICATION_CLIENT)。</p>
<p>4-指向 pdc ！PDC_14F_TRIAGE 结构。</p>
0x2:弹性客户端未能响应。
<p>3-复原客户端指向 (pdc ！ _PDC_RESILIENCY_CLIENT)。</p>
<p>4-指向 pdc ！PDC_14F_TRIAGE 结构。</p>
0x3:激活器客户端保留的时间太长的引用
<p>3-激活客户端指向 (pdc ！ _PDC_ACTIVATOR_CLIENT)。</p>
<p>4-指向 pdc ！PDC_14F_TRIAGE 结构。</p></td>
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

 

 

 




