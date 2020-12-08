---
title: Bug 检查 0x121 DRIVER_VIOLATION
description: DRIVER_VIOLATION bug 检查的值为0x00000121。 此 bug 检查表明驱动程序导致了冲突。
keywords:
- Bug 检查 0x121 DRIVER_VIOLATION
- DRIVER_VIOLATION
ms.date: 10/08/2019
topic_type:
- apiref
api_name:
- DRIVER_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: eb3dfbb38158bc762512a3550678ebe3773f3cec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837007"
---
# <a name="bug-check-0x121-driver_violation"></a>Bug 检查0x121：驱动程序 \_ 冲突

驱动程序 \_ 冲突 bug 检查的值为0x00000121。 此 bug 检查表明驱动程序导致了冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="driver_violation-parameters"></a>驱动程序 \_ 冲突参数

参数1指示违规类型。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1</p></td>
<td align="left"><p>当前 IRQL。</p></td>
<td align="left"><p>所需的 IRQL。</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>驱动程序调用了只能在特定 IRQL 上调用的函数。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

使用内核调试器并查看调用堆栈以确定导致冲突的驱动程序的名称： " [**！分析**](-analyze.md) " 调试扩展显示有关 bug 检查的信息，可帮助确定根本原因，然后输入一个 " [**k (" 显示堆栈 Backtrace ")**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令，以查看调用堆栈。
