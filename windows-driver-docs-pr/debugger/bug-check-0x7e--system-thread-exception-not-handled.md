---
title: Bug 检查 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
description: SYSTEM_THREAD_EXCEPTION_NOT_HANDLED bug 检查的值为0x0000007E。 此 bug 检查指示系统线程生成了错误处理程序未捕获的异常。
ms.assetid: 2ecea74f-21d6-4436-beed-d8cf8ef6b169
keywords:
- Bug 检查 0x7E SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
ms.date: 03/15/2019
topic_type:
- apiref
api_name:
- SYSTEM_THREAD_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a503ecbbc796f182b1915283f41368d9d7ef755e
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025317"
---
# <a name="bug-check-0x7e-system_thread_exception_not_handled"></a>Bug 检查 0x7E：系统\_线程\_异常未\_处理\_


系统\_线程\_异常\_未处理bug检查的值为0x0000007e。\_ 此 bug 检查指示系统线程生成了错误处理程序未捕获的异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户, 请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="system_thread_exception_not_handled-parameters"></a>系统\_线程\_异常\_未处理的参数\_

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
<td align="left"><p>未处理的异常代码</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>发生异常的地址</p></td>
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

"系统\_线程\_异常\_未\_处理 bug 检查" 指示系统线程生成了错误处理程序未捕获的异常。 若要对其进行解释, 必须确定生成的异常。

常见的异常代码包括:

- 数0x80000002状态\_数据\_类型不一致表明遇到了未对齐的数据引用。

- 0x80000003:状态\_断点指示在没有内核调试器附加到系统时遇到断点或断言。

- 0XC0000005状态\_访问\_冲突指示发生了内存访问冲突。

有关异常代码的完整列表, 请参阅位于 Microsoft Windows 驱动程序工具包 (WDK) 的 inc 目录中的 Ntstatus .h 文件。

<a name="resolution"></a>分辨率
----------

如果打算调试此问题, 参数 2 (异常地址) 应标识导致此问题的驱动程序或函数。

如果在 bug 检查消息中按名称列出了驱动程序, 请禁用或删除该驱动程序。 如果将此问题缩小到单个驱动程序, 请在代码中设置断点和单步来处理故障, 并深入了解导致崩溃的事件。

[ **! 分析**](-analyze.md)调试扩展显示有关 bug 检查的信息, 可帮助确定根本原因。 

可以使用[ **! 线程**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread)扩展以及[**dds、dps、dqs**](https://docs.microsoft.com/windows-hardware/drivers/debugger/dds--dps--dqs--display-words-and-symbols-)命令完成其他分析。 当 WinDbg 报告 "可能由以下原因导致" 时, 这可能是一个合理的方法: ntkrnlmp 

如果发生异常代码 0x80000003, 则会命中硬编码断点或断言, 但系统是使用 **/NODEBUG**开关启动的。 此问题不会频繁出现。 如果它反复发生, 请确保已连接内核调试器, 并使用 **/debug**开关启动系统。

如果发生异常代码数 0x80000002, 陷阱帧会提供其他信息。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用! 分析扩展](using-the--analyze-extension.md)和[! 分析](-analyze.md)

<a name="remarks"></a>备注
----------

如果你不具备使用 Windows 调试器来处理此问题, 则应使用一些基本的故障排除方法。

- 检查中的系统日志事件查看器是否有其他错误消息, 这些错误消息可能有助于识别导致 bug 检查0x7E 的设备或驱动程序。

- 如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

- 咨询硬件供应商以了解是否有任何 ACPI 或其他固件更新。 硬件问题 (如系统不兼容、内存冲突和 IRQ 冲突) 也可能生成此错误。

- 还可以禁用 BIOS 的内存缓存/阴影, 尝试解决错误。 还应运行系统制造商提供的硬件诊断。

- 确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如, 可以在[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

- 有关其他常规疑难解答信息, 请参阅[**蓝屏数据**](blue-screen-data.md)。
