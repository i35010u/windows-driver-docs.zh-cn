---
title: Bug 检查 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION bug 检查具有 0x0000003B 值。 这表示对特权代码从非特权代码执行的例程的转换时，发生异常。
ms.assetid: 0e2c230e-d942-4f32-ae8e-7a54aceb4c19
keywords:
- Bug 检查 0x3B SYSTEM_SERVICE_EXCEPTION
- SYSTEM_SERVICE_EXCEPTION
ms.date: 09/12/2018
topic_type:
- apiref
api_name:
- SYSTEM_SERVICE_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 022950eb69951b70c4b514b961385d3c90a92e61
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564105"
---
# <a name="bug-check-0x3b-systemserviceexception"></a>Bug 检查 0x3B：SYSTEM\_SERVICE\_EXCEPTION


系统\_服务\_异常错误检查的值为 0x0000003B。 这表示对特权代码从非特权代码执行的例程的转换时，发生异常。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="systemserviceexception-parameters"></a>系统\_服务\_异常参数


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
<td align="left"><p>导致异常的 bug 检查。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致 bug 检查指令的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>导致异常的错误检查的上下文记录的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

停止代码表示执行代码必须异常和低于，线程是一个系统线程。

其中一个参数中返回的异常信息被列入[NTSTATUS 值](https://msdn.microsoft.com/library/cc704588.aspx)，也可在 ntstatus.h 文件位于 Windows 驱动程序工具包 inc 目录中。 

一个可能的异常值是 0xC0000005:状态\_访问\_冲突 

这意味着内存访问冲突发生。 

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。

有关详细信息，请参阅以下主题：

[故障转储分析使用 Windows 调试器 (WinDbg)](crash-dump-files.md)

[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用 ！ 分析扩展](using-the--analyze-extension.md)和[！ 分析](-analyze.md)


在过去，此错误已链接到过多分页的池使用情况，由于用户模式下的图形驱动程序交叉并传递错误数据到内核代码可能导致。 如果您怀疑这种情况，使用中的 driver verifier 的池选项以收集其他信息。

<a name="resolution"></a>分辨率
----------

**若要调试此问题：** 使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令参数 3 中，并使用[ **kb （显示堆栈回溯）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。 此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。

有关一般故障排除 Windows bug 检查代码，请按照以下建议：

-   如果你最近添加到系统中，请尝试删除或替换它的硬件。 或者，请与制造商联系，以了解是否有任何修补程序。

-   如果最近，添加新设备驱动程序或系统服务尝试删除或更新它们。 尝试确定导致新的错误检查代码才会显示在系统中更改的内容。

-   查找范围**设备管理器**若要查看的任何设备都带有感叹号 （！）。 查看任何错误的驱动程序的驱动程序属性中显示的事件日志。 请尝试更新相关的驱动程序。

-   检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

 

 




