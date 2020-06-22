---
title: Bug 检查 0x3B SYSTEM_SERVICE_EXCEPTION
description: SYSTEM_SERVICE_EXCEPTION Bug 检查具有 0x0000003B 值。 这表示在执行从非特权代码转换为特权代码的例程时发生了异常。
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
ms.localizationpriority: high
ms.openlocfilehash: 1ee9898b747fe08032107845c2167414eabca5e6
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534638"
---
# <a name="bug-check-0x3b-system_service_exception"></a>Bug 检查 0x3B：SYSTEM\_SERVICE\_EXCEPTION

The SYSTEM\_SERVICE\_EXCEPTION Bug 检查具有 0x0000003B 值。 这表示在执行从非特权代码转换为特权代码的例程时发生了异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="system_service_exception-parameters"></a>SYSTEM\_SERVICE\_EXCEPTION 参数

<table>
<colgroup>
<col width="20%" />
<col width="80%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>导致 Bug 检查的异常。 </p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致 Bug 检查的指令的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>导致 Bug 检查的异常的上下文记录的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>


<a name="cause"></a>原因
-----

此停止代码指示执行代码存在异常，其下方的线程是系统线程。

[NTSTATUS 值](https://docs.microsoft.com/openspecs/windows_protocols/ms-erref/596a1078-e883-4972-9bbc-49e60bebca55)中介绍了在参数 1 中返回的异常信息。 异常代码在 ntstatus.h（[Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/)提供的标头文件）中定义  。 （有关详细信息，请参阅 [Windows 驱动程序工具包中的标头文件](../gettingstarted/header-files-in-the-windows-driver-kit.md)）。 

常见的异常代码包括：

- 0x80000003:STATUS\_BREAKPOINT

    没有内核调试器连接到系统时，遇到断点或 ASSERT。

- 0xC0000005:STATUS\_ACCESS\_VIOLATION

    出现内存访问冲突。 （Bug 检查的参数 4 是驱动程序尝试访问的地址。）

<a name="resolution"></a>解决方法
----------

若要调试此问题，请使用参数 3 的 [.cxr（显示上下文记录）](-cxr--display-context-record-.md) 命令，然后使用 [kb（显示堆栈回溯跟踪）](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)   。 还可以在此停止代码之前的代码中设置断点，并尝试单步前进到故障代码中。 使用 [u、ubuu (unassemble)](u--unassemble-.md) 命令查看程序集程序代码    。


[!analyze](-analyze.md) 调试程序扩展显示有关 bug 检查的信息，有助于确定根本原因  。 下面的示例是 !analyze 的输出  。

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

有关 WinDbg 和 !analyze 的详细信息，请参阅下列主题  ：

 - [使用 !analyze 扩展](using-the--analyze-extension.md) 

 - [使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

### <a name="identify-the-driver"></a>标识驱动程序

如果能够识别出导致错误的驱动程序，则它的名称将打印在蓝色屏幕上，并存储在该位置的内存中 (PUNICODE\_STRING) KiBugCheckDriver  。 可以使用一个调试器命令 [dx（显示调试器对象模型表达式）](dx--display-visualizer-variables-.md)来显示此内容：`dx KiBugCheckDriver` 。

使用 [!error](-error.md) 扩展显示参数 1 中的异常代码的相关信息  。 以下是 !error 的输出实例  。

```dbgcmd
2: kd> !error 00000000c0000005
Error code: (NTSTATUS) 0xc0000005 (3221225477) - The instruction at 0x%p referenced memory at 0x%p. The memory could not be %s.
```

请查看 WinDbg 的“堆栈文本”输出以获取故障发生时运行的内容的线索  。 如果有多个转储文件可用，请比较信息以查找堆栈中的通用代码。 使用调试器命令，如使用 [kb（显示堆栈回溯）](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)来调查错误代码  。

使用以下命令列出在内存中加载的模块：lm t n 

使用 !memusage 检查系统内存的一般状态  。 还可以使用命令 !pte 和 !pool 来检查内存的特定区域   。 

过去，此错误已链接到过度使用分页池，如果用户模式图形驱动程序交叉将错误数据传递到内核代码，则可能导致出现这种情况。 如果你怀疑就是这种情况，请使用驱动程序验证器中的池选项收集其他信息。

### <a name="driver-verifier"></a>驱动程序验证程序

驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 例如，驱动程序验证程序检查内存资源（如内存池）的使用。 如果在执行驱动程序代码时标识错误，它会主动创建一个异常，以允许进一步检查该部分驱动程序代码。 驱动程序验证程序管理器内置于 Windows 中，可在所有 Windows 电脑上使用。 

若要启动驱动程序验证程序管理器，请在命令提示下输入“验证程序”  。 你可以配置要验证的驱动程序。 验证驱动程序的代码在运行时会增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[驱动程序验证程序](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)。


<a name="remarks"></a>备注
-------

有关 Windows Bug 检查代码的一般故障排除，请按照以下建议操作：

-   如果最近添加了新的设备驱动程序或系统服务，请尝试删除或更新它们。 尝试确定系统中导致新 Bug 检查代码出现的原因。

-   查看设备管理器，了解是否有任何设备标记为惊叹号 (!)，这表示存在问题。 查看任何故障设备驱动程序的属性中显示的事件日志。 尝试更新相关驱动程序。

-   检查事件查看器中的系统日志，以获取可能有助于查明导致错误的设备或驱动程序的其他错误消息。 在系统日志中查找与蓝屏同时出现的严重错误。

-   如果最近向系统添加了硬件，请尝试删除或替换它。 或与制造商联系，查看是否有可用的修补程序。

有关其他常规疑难解答信息，请参阅[蓝屏数据](blue-screen-data.md)。
