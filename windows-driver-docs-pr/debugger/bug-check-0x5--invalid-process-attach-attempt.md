---
title: Bug 检查 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
description: INVALID_PROCESS_ATTACH_ATTEMPT bug 检查具有值为 0x00000005。
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
ms.openlocfilehash: ffea1e52291cf7484157ab29d003a25801549d99
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238368"
---
# <a name="bug-check-0x5-invalidprocessattachattempt"></a>Bug 检查 0x5：无效\_进程\_附加\_尝试


无效\_进程\_附加\_尝试错误检查的值为 0x00000005。 这通常表示在线程已附加到进程中的位置，不允许的情况。 例如，如果出现此 bug 检查可能**KeAttachProcess**线程是否已附加到的进程 （这是非法），或如果从返回的线程处于附加状态 （这是无效），调用特定的函数时调用

检查此错误极少出现。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="invalidprocessattachattempt-parameters"></a>无效\_进程\_附加\_尝试参数


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
<td align="left"><p>目标进程中，调度程序对象的指针，或者如果线程已经附加，原始进程对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>当前线程当前附加到进程的调度程序对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>线程的 APC 状态索引的值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>一个非零值指示 DPC 运行在当前处理器上。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果驱动程序调用，则会出现此 bug 检查**KeAttachProcess**函数和线程已附加到另一个进程。 最好使用**KeStackAttachProcess**函数。 如果当前线程是否已附加到另一个进程**KeStackAttachProcess**函数将保存当前的 APC 状态之前它将当前线程附加到新进程。

 

 




