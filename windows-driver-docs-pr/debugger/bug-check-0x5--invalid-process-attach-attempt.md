---
title: Bug 检查 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
description: INVALID_PROCESS_ATTACH_ATTEMPT bug 检查的值为0x00000005。
ms.assetid: 72efb88f-1bf7-4552-b44e-4ecb04754b7d
keywords:
- Bug 检查 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
- INVALID_PROCESS_ATTACH_ATTEMPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_PROCESS_ATTACH_ATTEMPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 663aabde692a1c0e27347914f589c328aa9113c5
ms.sourcegitcommit: 70c8e83900015eaea013fb742e5e137cfd08ca98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2020
ms.locfileid: "76885356"
---
# <a name="bug-check-0x5-invalid_process_attach_attempt"></a>Bug 检查0x5：附加\_尝试\_无效的\_进程


\_附加\_尝试 bug 检查的无效\_进程的值为0x00000005。 这通常表示在不允许的情况下，线程已附加到进程。 例如，如果在线程已附加到进程时调用了**KeAttachProcess** （这是非法的），或者如果从特定函数返回的线程处于附加状态（无效），则可能发生此 bug 检查。

此 bug 检查很少出现。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="invalid_process_attach_attempt-parameters"></a>\_进程无效\_附加\_尝试参数


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
<td align="left"><p>指向目标进程的调度程序对象的指针; 如果已附加线程，则为指向原始进程的对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>指向当前线程当前附加到的进程的调度程序对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>线程的 APC 状态索引的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>如果值为非零，则表示 DPC 正在当前处理器上运行。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
如果驱动程序调用**KeAttachProcess**函数，并且该线程已附加到另一个进程，则会发生此 bug 检查。 最好使用**KeStackAttachProcess**函数。 如果当前线程已附加到另一个进程，则**KeStackAttachProcess**函数将保存当前的 APC 状态，然后将当前线程附加到新进程。

 

 




