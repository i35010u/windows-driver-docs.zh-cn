---
title: Bug 检查 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION bug 检查具有 0x0000003B 值。 这表示对特权代码从非特权代码执行的例程的转换时，发生异常。
ms.assetid: 0e2c230e-d942-4f32-ae8e-7a54aceb4c19
keywords:
- Bug 检查 0x3B SYSTEM_SERVICE_EXCEPTION
- SYSTEM_SERVICE_EXCEPTION
ms.date: 03/24/2019
topic_type:
- apiref
api_name:
- SYSTEM_SERVICE_EXCEPTION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4cbd6a2202f9c2d7a3b3c15a4129a6663abbeda2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361905"
---
# <a name="bug-check-0x3b-systemserviceexception"></a>Bug 检查 0x3B：SYSTEM\_SERVICE\_EXCEPTION


系统\_服务\_异常错误检查的值为 0x0000003B。 这表示对特权代码从非特权代码执行的例程的转换时，发生异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。


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

其中一个参数中返回的异常信息被列入[NTSTATUS 值](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)，也可在 ntstatus.h 文件位于 Windows 驱动程序工具包 inc 目录中。 

常见的异常代码包括：

-   0x80000003:状态\_断点

    没有内核调试器已附加到系统时出现断点或断言。

-   0xC0000005:状态\_访问\_冲突

    出现内存访问冲突。 （检查错误的参数 4 是驱动程序尝试访问的地址。）

<a name="resolution"></a>分辨率
----------

**若要调试此问题：** 

使用[ **.cxr （显示上下文记录）** ](-cxr--display-context-record-.md)命令参数 3 中，并使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。 此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。 使用[u，ub，uu （反汇编）]()命令来查看程序集的程序代码。


[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

```
SYSTEM_SERVICE_EXCEPTION (3b)
An exception happened while executing a system service routine.
Arguments:
Arg1: 00000000c0000005, Exception code that caused the bugcheck
Arg2: fffff802328375b0, Address of the instruction which caused the bugcheck
Arg3: ffff9c0a746c2330, Address of the context record for the exception that caused the bugcheck
Arg4: 0000000000000000, zero.
...
```

有关详细信息，请参阅以下主题：

[使用 ！ 分析扩展](using-the--analyze-extension.md) 

[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。 可以使用调试器[ **dx （显示调试器对象模型表达式）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)命令来显示此- `dx KiBugCheckDriver`。

使用[！ 错误](-error.md)扩展名，即可在参数 1 中显示有关异常代码的信息。

```
2: kd> !error 00000000c0000005
Error code: (NTSTATUS) 0xc0000005 (3221225477) - The instruction at 0x%p referenced memory at 0x%p. The memory could not be %s.
```

在运行哪些程序发生失败时查看线索堆栈文本。 如果有多个转储文件，将信息查找是堆栈中的常见代码进行比较。 使用调试器命令，例如使用[ **kb （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)要调查的错误代码。

使用`lm t n`到内存中加载的模块列表。 

使用`!memusage`并检查系统内存的一般状态。 `!pte`和`!pool`命令还可用于检查特定区域的内存。 

在过去，此错误已链接到过多分页的池使用情况，由于用户模式下的图形驱动程序交叉并传递错误数据到内核代码可能导致。 如果您怀疑这种情况，使用中的 driver verifier 的池选项以收集其他信息。

**驱动程序验证程序**

驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 例如，驱动程序验证工具将检查内存资源，如内存池的使用。 如果它发现错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifer*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。


**时间的差旅跟踪**

如果可以按要求重现 bug 检查，调查花些时间旅行跟踪使用 WinDbg 预览的可能性。 有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。


<a name="remarks"></a>备注
----------

有关一般故障排除 Windows bug 检查代码，请按照以下建议：

-   如果最近，添加新设备驱动程序或系统服务尝试删除或更新它们。 尝试确定导致新的错误检查代码才会显示在系统中更改的内容。

-   查找范围**设备管理器**若要查看的任何设备都带有感叹号 （！）。 查看任何错误的驱动程序的驱动程序属性中显示的事件日志。 请尝试更新相关的驱动程序。

-   检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

-   如果你最近添加到系统中，请尝试删除或替换它的硬件。 或者，请与制造商联系，以了解是否有任何修补程序。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。


 

 




