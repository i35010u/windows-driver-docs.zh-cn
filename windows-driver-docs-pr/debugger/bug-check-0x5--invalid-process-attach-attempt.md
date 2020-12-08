---
title: Bug 检查 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
description: INVALID_PROCESS_ATTACH_ATTEMPT bug 检查的值为0x00000005。
keywords:
- Bug 检查 0x5 INVALID_PROCESS_ATTACH_ATTEMPT
- INVALID_PROCESS_ATTACH_ATTEMPT
ms.date: 09/04/2020
topic_type:
- apiref
api_name:
- INVALID_PROCESS_ATTACH_ATTEMPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24bf877a3d02d39a833b2d849545ef878fc2e8b6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786477"
---
# <a name="bug-check-0x5-invalid_process_attach_attempt"></a>Bug 检查0x5： \_ 进程 \_ 附加 \_ 尝试无效


无效的 \_ 进程 \_ 附加 \_ 尝试 bug 检查的值为0x00000005。 这通常表示在不允许的情况下，线程已附加到进程。 例如，如果在线程已附加到 (这是非法) 的进程时调用了 **KeAttachProcess** ，或者从特定函数返回的线程在附加状态下调用， (这是无效的) ，则会发生此 bug 检查。

此 bug 检查很少出现。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="invalid_process_attach_attempt-parameters"></a>无效的 \_ 进程 \_ 附加 \_ 尝试参数


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

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

如果驱动程序调用 [KeAttachProcess](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-keattachprocess)  函数，并且该线程已附加到另一个进程，则会发生此 bug 检查。 最好使用 [KeStackAttachProcess](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestackattachprocess) 函数。 如果当前线程已附加到另一个进程，则 **KeStackAttachProcess** 函数将保存当前的 APC 状态，然后将当前线程附加到新进程。 错误调用 **KeStackAttachProcess** 也会导致此错误检查，例如，当 DPC 正在当前处理器上运行时。

有关此方面的常规信息，请参阅使用 [Windows Kernel-Mode 进程和线程管理器](../kernel/windows-kernel-mode-process-and-thread-manager.md) 和 [内核调度程序对象简介](../kernel/managing-interlocked-queues-with-a-driver-created-thread.md)。

 

