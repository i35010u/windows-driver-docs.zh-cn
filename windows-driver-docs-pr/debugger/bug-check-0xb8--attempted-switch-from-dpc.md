---
title: Bug 检查 0xB8 ATTEMPTED_SWITCH_FROM_DPC
description: ATTEMPTED_SWITCH_FROM_DPC bug 检查具有 0x000000B8 值。 这表示延迟的过程调用 (DPC) 例程尝试进行非法操作。
ms.assetid: 614b7be8-cec9-4dd9-b183-66db1790c31f
keywords:
- Bug 检查 0xB8 ATTEMPTED_SWITCH_FROM_DPC
- ATTEMPTED_SWITCH_FROM_DPC
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_SWITCH_FROM_DPC
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a10692220e22a2605faedcf4f92b440142106510
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238404"
---
# <a name="bug-check-0xb8-attemptedswitchfromdpc"></a>Bug 检查 0xB8：尝试\_交换机\_FROM\_DPC


已尝试\_交换机\_FROM\_DPC bug 检查的值为 0x000000B8。 这表示延迟的过程调用 (DPC) 例程尝试进行非法操作。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="attemptedswitchfromdpc-parameters"></a>尝试\_交换机\_FROM\_DPC 参数


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
<td align="left"><p>1</p></td>
<td align="left"><p>原始线程导致了故障</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>新线程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>原始线程堆栈地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

一个等待操作，附加进程，或者，yield 试图从 DPC 例程。 这是非法操作。

<a name="resolution"></a>分辨率
----------

导致错误的原始 DPC 例程中的代码将导致的堆栈跟踪。

 

 




