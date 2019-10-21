---
title: Bug 检查 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION bug 检查的值为0x0000003B。 这表示执行从非特权代码转换为特权代码的例程时发生了异常。
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
ms.openlocfilehash: 9f92b529d19650ff18e9faff211131bfbd86eee4
ms.sourcegitcommit: 6d7f25f280af5fd4f4d9337d131c2a22288847fc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359582"
---
# <a name="bug-check-0x3b-system_service_exception"></a>Bug 检查0x3B： SYSTEM \_SERVICE \_EXCEPTION

系统 \_SERVICE \_EXCEPTION bug 检查的值为0x0000003B。 这表示执行从非特权代码转换为特权代码的例程时发生了异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="system_service_exception-parameters"></a>系统 \_SERVICE \_EXCEPTION 参数

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
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
<td align="left"><p>导致 bug 检查的异常。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致 bug 检查的指令的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>引发 bug 检查的异常的上下文记录的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

此 stop 代码指示执行代码有一个异常，其下的线程是系统线程。

在[NTSTATUS 值](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)中介绍了在参数1中返回的异常信息。 异常代码在*ntstatus*中定义，该文件是[Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/)提供的标头文件。 （有关详细信息，请参阅[Windows 驱动程序工具包中的标头文件](../gettingstarted/header-files-in-the-windows-driver-kit.md)）。 

常见的异常代码包括：

- 0x80000003：状态 \_BREAKPOINT

    当没有内核调试器附加到系统时遇到断点或断言。

- 0xC0000005：状态 \_ACCESS \_VIOLATION

    发生了内存访问冲突。 （Bug 检查的参数4是驱动程序尝试访问的地址。）

<a name="resolution"></a>分辨率
----------

若要调试此问题，请使用参数为3的[ **.cxr** （显示上下文记录）](-cxr--display-context-record-.md)命令，然后使用[ **kb** （显示 stack backtrace）](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)。 你还可以在代码中设置一个断点，该断点位于此 stop 代码之前，并尝试单步执行错误代码。 使用[ **u**、 **ub**、 **uu** （unassemble）](u--unassemble-.md)命令查看程序集程序代码。


[ **！分析**](-analyze.md)调试器扩展显示有关 bug 检查的信息，可帮助确定根本原因。 下面的示例是来自 **！分析**的输出。

```dbgcmd
SYSTEM_SERVICE_EXCEPTION (3b)
An exception happened while executing a system service routine.
Arguments:
Arg1: 00000000c0000005, Exception code that caused the bugcheck
Arg2: fffff802328375b0, Address of the instruction which caused the bugcheck
Arg3: ffff9c0a746c2330, Address of the context record for the exception that caused the bugcheck
Arg4: 0000000000000000, zero.
...
```

有关 WinDbg 和 **！分析**的详细信息，请参阅以下主题：

 - [使用！分析扩展](using-the--analyze-extension.md) 

 - [使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

### <a name="identify-the-driver"></a>确定驱动程序

如果可以识别负责错误的驱动程序，则其名称将打印在蓝屏上，并存储在内存中的位置（PUNICODE \_STRING） **KiBugCheckDriver**。 可以使用[ **dx** （显示调试器对象模型表达式）](https://docs.microsoft.com/windows-hardware/drivers/debugger/dx--display-visualizer-variables-)和调试器命令来显示此内容： `dx KiBugCheckDriver`。

使用[ **！ error**](-error.md)扩展显示有关参数1中的异常代码的信息。 下面是来自 **！ error**的输出示例。

```dbgcmd
2: kd> !error 00000000c0000005
Error code: (NTSTATUS) 0xc0000005 (3221225477) - The instruction at 0x%p referenced memory at 0x%p. The memory could not be %s.
```

查看 WinDbg 的**堆栈文本**输出，以获取有关发生故障时正在运行的内容的线索。 如果有多个转储文件可用，则比较它们的信息以查找堆栈中的通用代码。 使用诸如[ **kb** （显示 stack backtrace）](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)之类的调试器命令调查错误代码。

使用以下命令列出在内存中加载的模块： **lm t n**

使用 **！ memusage**检查系统内存的一般状态。 你还可以使用命令 **！ pte**和 **！池**来检查内存的特定区域。 

过去，此错误已链接到过度使用页面缓冲池，这可能是由于用户模式图形驱动程序与内核代码交叉并向内核代码传递错误数据导致的。 如果怀疑出现这种情况，请使用驱动程序验证器中的池选项收集更多信息。

### <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序是一种实时运行的工具，用于检查驱动程序的行为。 例如，驱动程序验证程序检查内存资源的使用情况，例如内存池。 如果它标识了驱动程序代码执行过程中的错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证程序管理器内置于 Windows 中，在所有 Windows Pc 上都可用。 

若要启动驱动程序验证程序管理器，请在命令提示符下输入**验证**程序。 你可以配置要验证的驱动程序。 验证驱动程序的代码会在运行时增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。


<a name="remarks"></a>备注
-------

有关 Windows 错误检查代码的一般疑难解答，请遵循以下建议：

-   如果最近添加了新的设备驱动程序或系统服务，请尝试删除或更新它们。 尝试确定系统中发生了导致新 bug 检查代码的更改。

-   查看设备管理器，查看是否有任何设备标记为惊叹号（！），这表示存在问题。 查看显示在任何错误设备驱动程序的属性中的事件日志。 尝试更新相关驱动程序。

-   检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 在与蓝色屏幕相同的时间范围内查找系统日志中的严重错误。

-   如果最近向系统中添加了硬件，请尝试删除或替换它。 或与制造商联系，查看是否有可用的修补程序。

有关其他常规疑难解答信息，请参阅[蓝屏数据](blue-screen-data.md)。
