---
title: Bug 检查 0x121 DRIVER_VIOLATION
description: DRIVER_VIOLATION bug 检查的值为0x00000121。 此 bug 检查表明驱动程序导致了冲突。
ms.assetid: 4a5d1d84-a958-45a6-9511-b5b4ecd4c067
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
ms.openlocfilehash: 95dd279e70ce0fbb3e98b00c5e826c078ac7a396
ms.sourcegitcommit: c2a96138fe8d619c2d2591cd849ae2dd4bb6c37b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2020
ms.locfileid: "77260501"
---
# <a name="bug-check-0x121-driver_violation"></a>Bug 检查0x121：驱动程序\_冲突

驱动程序\_违反 bug 检查的值为0x00000121。 此 bug 检查表明驱动程序导致了冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="driver_violation-parameters"></a>驱动程序\_冲突参数

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
<td align="left"><p>保留</p></td>
<td align="left"><p>驱动程序调用了只能在特定 IRQL 上调用的函数。</p></td>
</tr>
</tbody>
</table>

<a name="remarks"></a>备注
-------

使用内核调试器并查看调用堆栈以确定导致冲突的驱动程序的名称： [ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因，然后输入[**k （显示 stack Backtrace）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)命令之一来查看调用堆栈。
