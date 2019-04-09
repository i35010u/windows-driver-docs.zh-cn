---
title: Bug Check 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
description: SYSTEM_THREAD_EXCEPTION_NOT_HANDLED bug 检查具有 0x0000007E 值。 此 bug 检查指示系统线程生成的错误处理程序未捕获异常。
ms.assetid: 2ecea74f-21d6-4436-beed-d8cf8ef6b169
keywords:
- Bug Check 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
ms.date: 03/15/2019
topic_type:
- apiref
api_name:
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ae805605e03e4ac29c6784949351a9bb4de679f3
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239471"
---
# <a name="bug-check-0x7e-systemthreadexceptionnothandled"></a>Bug 检查 0x7E：系统\_线程\_异常\_不\_已处理


系统\_线程\_异常\_不\_已处理错误检查的值为 0x0000007E。 此 bug 检查指示系统线程生成的错误处理程序未捕获异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="systemthreadexceptionnothandled-parameters"></a>系统\_线程\_异常\_不\_HANDLED 参数


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
<td align="left"><p>未处理异常代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>异常发生位置的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>异常记录的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>上下文记录的地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

系统\_线程\_异常\_不\_HANDLED bug 检查指示系统线程生成的错误处理程序未捕获异常。 若要解释它，必须标识生成的异常。

常见的异常代码如下所示：

-   数 0x80000002:状态\_数据类型\_未对齐指示遇到了未对齐的数据引用。

-   0x80000003:状态\_断点指示没有内核调试器已附加到系统时出现断点或断言。

-   0xC0000005:状态\_访问\_冲突指示内存访问冲突发生。

异常代码的完整列表，请参阅位于 inc 目录的 Microsoft Windows Driver Kit (WDK) 中的 Ntstatus.h 文件。

<a name="resolution"></a>分辨率
----------

如果您计划调试此问题，应确定参数 2 （异常地址），驱动程序或导致此问题的函数。

如果驱动程序列出的 bug 检查消息中的名称，请禁用或删除该驱动程序。 如果此问题缩小到单个驱动程序，设置断点和单单步在代码中工作，以定位故障，并深入了解导致故障事件。

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。 

可以执行其他分析使用[ **！ 线程**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread)扩展，并将[ **dds，dps，dqs** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/dds--dps--dqs--display-words-and-symbols-)命令。 WinDbg 报告时，这可能是合理的方法"可能造成的： ntkrnlmp.exe" 

如果出现异常代码 0x80000003，硬编码断点或断言已命中，但在系统启动时采用了 **/NODEBUG**切换。 不应经常出现此问题。 如果重复发生，请确保将内核调试程序连接并启动系统，并且使用 **/debug**切换。

如果发生异常的代码数 0x80000002，陷阱框架提供的其他信息。


有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用 ！ 分析扩展](using-the--analyze-extension.md)和[！ 分析](-analyze.md)


**时间的差旅跟踪**

如果可以按要求重现 bug 检查，调查花些时间旅行跟踪使用 WinDbg 预览的可能性。 有关详细信息，请参阅[时间旅行调试-概述](time-travel-debugging-overview.md)。


<a name="remarks"></a>备注
----------

如果您不准备使用 Windows 调试器处理此问题，则应使用一些基本的故障排除方法。

-   有关其他错误消息可能有助于识别设备或驱动程序导致 bug 检查 0x7E 检查事件查看器中的系统日志。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   请咨询硬件供应商任何 ACPI 或其他固件更新。 硬件问题，例如系统的不兼容性、 内存冲突和 IRQ 冲突还可以生成此错误。

-   此外可以禁用内存缓存/隐藏的 BIOS 来尝试解决该错误。 您还应运行硬件诊断程序，系统制造商提供。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。


 




