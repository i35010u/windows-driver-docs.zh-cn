---
title: 蓝屏数据
description: 当 Microsoft Windows 遇到损害安全系统操作的情况时，系统将会挂起。 此条件称为 "bug 检查" 或 "停止" 错误。
keywords:
- 蓝屏数据 Windows 调试
ms.date: 01/29/2021
topic_type:
- apiref
api_name:
- Blue Screen Data
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b679aecc7d6d9733529c251ec4bb31e6b80ce839
ms.sourcegitcommit: 91632914d86484a6ab6340b04c1ee2d92ff7cf09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/04/2021
ms.locfileid: "99534279"
---
# <a name="blue-screen-data"></a>蓝屏数据

**注意**  本主题适用于程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://support.microsoft.com/help/14238/windows-10-troubleshoot-blue-screen-errors)。

**注意**   如果你是 IT 专业人员或支持代理，请参阅此文，了解其他信息、 [排查 "蓝屏" 问题或停止错误问题，然后再联系 Microsoft 支持部门](https://support.microsoft.com/help/3106831/)。

当 Microsoft Windows 遇到损害安全系统操作的情况时，系统将会挂起。 此条件称为 " *bug 检查*"。 通常也称为 *系统崩溃*、 *内核错误* 或 *停止错误*。

如果在操作系统完整性泄露后允许操作系统继续运行，则它可能会损坏数据或危及系统的安全。

如果系统上启用了故障转储，则会创建故障转储文件。

如果内核调试器已附加并且处于活动状态，则系统会导致中断，以便可以使用调试器来调查故障。

如果未附加调试器，则会出现蓝色文本屏幕，其中包含有关错误的信息。 此屏幕称为 *蓝屏*、 *bug 检查屏幕* 或 *停止屏幕*。

如果使用的是 Windows 的内部版本，则会在绿色背景上显示文本。

蓝屏的确切外观取决于错误的原因。

下面是一个可能的蓝屏的示例：

![bug 检查示例 windows 10 blue screen with qr 代码](images/bug-check-example-blue-screen-page-fault.png)

在 [**\_ \_ \_ 非分页 \_ 区域**](bug-check-0x50--page-fault-in-nonpaged-area.md)显示 stop 代码，如页错误。 当它可用时，还会显示正在执行的代码的模块名称，如 AcmeVideo.sys。

如果已写入 [内核模式转储文件](kernel-mode-dump-files.md) ，则会在写入转储时，按百分比完成计数来指示这一点。

与 " [Bug 检查代码参考](bug-check-code-reference2.md)" 中列出的每个 "stop" 代码相关联的停止代码十六进制值。

## <a name="gathering-the-stop-code-parameters"></a>正在收集停止代码参数

每个 bug 检查代码都具有四个提供附加信息的关联参数。 每个 stop 代码的 [Bug 检查代码引用](bug-check-code-reference2.md) 中介绍了这些参数。

有多种方法可以收集四个停止代码参数。

-   在事件查看器中检查 Windows 系统日志。 错误检查的事件属性将列出四个停止代码参数。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。

-   加载生成的转储文件，并在附加调试器中使用 [**！ "分析**](-analyze.md) " 命令。 有关详细信息，请参阅 [使用 WinDbg 分析 Kernel-Mode 转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)。

-   将内核调试器附加到出错的 PC。 当发生停止代码时，调试器输出将在停止代码十六进制值之后包含四个参数。

    ```dbgcmd
    *******************************************************************************
    *                                                                             *
    *                        Bugcheck Analysis                                    *
    *                                                                             *
    *******************************************************************************

    Use !analyze -v to get detailed debugging information.

    BugCheck 9F, {3, ffffe000f38c06a0, fffff803c596cad0, ffffe000f46a1010}

    Implicit thread is now ffffe000`f4ca3040
    Probably caused by : hidusb.sys
    ```

### <a name="span-idbug_check_symbolic_namesspanspan-idbug_check_symbolic_namesspanbug-check-symbolic-names"></a><span id="bug_check_symbolic_names"></span><span id="BUG_CHECK_SYMBOLIC_NAMES"></span>Bug 检查符号名称

[**驱动程序 \_电源 \_ 状态 \_ 故障**](bug-check-0x9f--driver-power-state-failure.md) 是错误检查符号名称，其关联 Bug 检查代码为9f。 与 Bug 检查符号名称关联的停止代码十六进制值列在 " [Bug 检查代码参考](bug-check-code-reference2.md)" 中。

### <a name="span-idreading_bug_check_information_from_the_debuggerspanspan-idreading_bug_check_information_from_the_debuggerspanreading-bug-check-information-from-the-debugger"></a><span id="reading_bug_check_information_from_the_debugger"></span><span id="READING_BUG_CHECK_INFORMATION_FROM_THE_DEBUGGER"></span>从调试器读取 Bug 检查信息

如果附加了调试器，则 bug 检查将导致目标计算机中断到调试器。 在这种情况下，蓝屏可能不会立即出现，此故障的完整详细信息将发送到调试器并显示在调试器窗口中。 若要第二次查看此信息，请使用 [**错误检查 (显示 Bug 检查数据)**](-bugcheck--display-bug-check-data-.md) 命令或 " [**！分析**](-analyze.md) 扩展" 命令。

## <a name="kernel-debugging-and-crash-dump-analysis"></a>内核调试和故障转储分析

当其他故障排除方法失败或反复发生问题时，内核调试特别有用。 请记得捕获错误消息的 "bug 检查信息" 部分中的确切文本。 若要隔离复杂问题并制定可行的解决方法，请记录导致失败的确切操作。

[!analyze](-analyze.md) 调试扩展显示有关 bug 检查的信息，并有助于确定根本原因  。

你还可以在代码中设置一个断点，使其导致此 stop 代码，并尝试单步执行出错的代码。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用！分析扩展](using-the--analyze-extension.md) 和 [！分析](-analyze.md)

在第9频道上显示的碎片整理工具- <https://channel9.msdn.com/Shows/Defrag-Tools>

## <a name="using-driver-verifier-to-gather-information"></a>使用驱动程序验证器收集信息

据估计，蓝屏的三个季度由错误驱动程序引起。 驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 例如，驱动程序验证程序检查内存资源（如内存池）的使用。 如果发现驱动程序代码执行过程中出现错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证程序管理器内置于 Windows 中，可在所有 Windows PC 上使用。 若要启动驱动程序验证程序管理器，请在命令提示下键入“验证程序”  。 你可以配置要验证的驱动程序。 验证驱动程序的代码在运行时会增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。

## <a name="tips-for-software-engineers"></a>软件工程师的技巧

当 bug 检查作为你编写的代码的结果发生时，你应该使用内核调试器来分析问题，然后修复代码中的 bug。 有关完整详细信息，请参阅 [Bug 检查代码参考](bug-check-code-reference2.md) 部分中的各个 bug 检查代码。

但是，您可能还会遇到不是由您自己的代码所导致的 bug 检查。 在这种情况下，你可能无法修复问题的实际原因，因此你的目标应该是解决该问题，如果可能，请隔离并删除出错的硬件或软件组件。

许多问题可以通过基本的故障排除过程来解决，如验证指令、重新安装关键组件和验证文件日期。 此外，事件查看器 Sysinternals 诊断工具和网络监视工具可能会隔离并解决这些问题。

有关 Windows 错误检查代码的一般疑难解答，请遵循以下建议：

-   如果最近向系统中添加了硬件，请尝试删除或替换它。 或与制造商联系，查看是否有可用的修补程序。

-   如果最近添加了新的设备驱动程序或系统服务，请尝试删除或更新它们。 尝试确定系统中发生了导致新 bug 检查代码的更改。

-   查看 **Device Manager** 查看是否有任何设备标记为惊叹号 (！ ) 。 查看在驱动程序属性中显示的任何错误驱动程序的事件日志。 请尝试更新相关驱动程序。

-   检查中的系统日志事件查看器是否有其他错误消息，这些错误消息可能有助于找出导致错误的设备或驱动程序。 有关详细信息，请参阅[打开事件查看器](https://support.microsoft.com/hub/4338813/windows-help#1TC=windows-7)。 在系统日志中查找与蓝屏同时出现的严重错误。

-   你可以尝试运行系统制造商提供的硬件诊断。

-   运行 Windows 内存诊断工具来测试内存。 在 "控制面板" 搜索框中键入 "内存"，然后选择 " **诊断计算机的内存问题**"。运行测试后，使用事件查看器查看系统日志下的结果。 查找“内存诊断结果”条目以查看结果  。

-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

-   运行病毒检测程序。 病毒可能会感染为 Windows 格式化的所有类型的硬盘，导致磁盘损坏可能生成系统 bug 检查代码。 请确保病毒检测程序检查主启动记录中是否有病毒感染。

-   使用扫描磁盘实用工具确认没有文件系统错误。 选择并按住 (或右键单击要扫描的驱动器) ，然后选择 " **属性**"。 选择 " **工具**"。 选择 " **立即检查** " 按钮。

-   使用系统文件检查器工具修复丢失或损坏的系统文件。 系统文件检查器是 Windows 中的一个实用工具，它允许用户在 Windows 系统文件中扫描损坏并还原损坏的文件。 使用以下命令 ( # A0) 运行系统文件检查器工具。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅 [使用系统文件检查器工具修复丢失或损坏的系统文件](https://support.microsoft.com/help/929833/use-the-system-file-checker-tool-to-repair-missing-or-corrupted-system)。

-   确认硬盘上有足够的可用空间。 操作系统和某些应用程序需要足够的可用空间来创建交换文件和其他功能。 根据系统配置，具体要求会有所不同，但通常最好使用10% 到15% 的可用空间。

-   验证系统是否已安装最新的 Service Pack。 若要检测系统上安装的 Service Pack （如果有），请选择 " **开始**"，选择 " **运行**"，键入 **winver**，然后按 enter。 " **关于 windows** " 对话框显示 windows 版本号和 Service Pack 的版本号（如果已安装）。

-   请与制造商联系，查看是否有更新的系统 BIOS 或固件可用。

-   禁用 BIOS 内存选项，例如缓存或隐藏。

-   对于 Pc，请确保所有扩展卡都已正确固定并且所有电缆都已完全连接。

**使用安全模式**

删除或禁用组件时，请考虑使用安全模式。 使用安全模式仅加载 Windows 启动过程中所需的最少驱动程序和系统服务。 若要进入安全模式，请使用 "设置" 中的 " **更新和安全** "。 选择 "**恢复** - &gt; **高级启动**" 以启动到维护模式。 在出现的菜单中，**选择 "** - &gt; **高级选项**" "启动  - &gt; **设置**  - &gt; **重新启动**"。 Windows 重启到 " **启动设置** " 屏幕后，选择 "选项"、"4"、"5" 或 "6" 以启动到安全模式。

可以通过在启动时按功能键来提供安全模式，例如 F8。 请参阅制造商提供的有关特定启动选项的信息。

