---
title: Bug 检查 0x2B PANIC_STACK_SWITCH
description: PANIC_STACK_SWITCH bug 检查具有 0x0000002B 值。 这表示内核模式堆栈已溢出。
ms.assetid: 0ab28a16-979d-4b40-812a-a31fac3f6be8
keywords:
- Bug 检查 0x2B PANIC_STACK_SWITCH
- PANIC_STACK_SWITCH
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PANIC_STACK_SWITCH
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0572fd89535adc906ed8f16cc9bcaec1017d73b7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902527"
---
# <a name="bug-check-0x2b-panicstackswitch"></a>Bug 检查 0x2B：PANIC\_堆栈\_开关


PANIC\_堆栈\_交换机 bug 检查的值为 0x0000002B。 这表示内核模式堆栈已溢出。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="panicstackswitch-parameters"></a>PANIC\_堆栈\_开关参数


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
<td align="left"><p>陷阱帧</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

内核模式驱动程序使用太多堆栈空间，则通常会出现此错误。 它也会出现严重的数据损坏时在内核中。


## <a name="resolution"></a>分辨率
[ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关错误检查的信息，有助于在确定根本原因。
 

 




