---
title: 蓝屏数据
description: 当 Microsoft Windows 遇到一个条件，从而危及安全系统的状态时，系统就会停止。 这种情况称为 bug 检查或停止错误。
ms.assetid: 8cc42643-e231-49dd-96b0-6cb528d5d7a9
keywords:
- 蓝色的屏幕数据 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Blue Screen Data
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a7886c3cbb5b66cc18c67511eb4b601ab195c850
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59239176"
---
# <a name="blue-screen-data"></a>蓝屏数据


**请注意**  本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://go.microsoft.com/fwlink/p/?linkid=183646)。

 

**请注意**  如果你是 IT 专业人员或支持代理，请参阅本文的其他信息，了解[或进行故障排除"蓝屏"停止错误问题之前联系 Microsoft 支持部门](https://support.microsoft.com/help/3106831/troubleshoot-blue-screen-or-stop-error-problems-before-you-contact-microsoft-support)。

 

当 Microsoft Windows 遇到一个条件，从而危及安全系统的状态时，系统就会停止。 这种情况称为*bug 检查*。 它通常也称为*系统崩溃*即*内核错误*，或*停止错误*。

如果操作系统允许操作系统完整性遭到破坏之后继续运行，它可能损坏数据或危及系统安全。

如果在系统上启用了故障转储，创建的崩溃转储文件。

如果内核调试器已附加并处于活动状态，系统会引发一个分行符，以便可以使用调试器来调查在发生崩溃。

如果未附加调试器，蓝色文本屏幕会显示有关错误的信息。 调用此屏幕*蓝屏*即*bug 检查屏幕*，或*停止屏幕*。

如果使用 Windows 预览体验内部版本，将绿色背景上显示的文本。

蓝色屏幕的确切外观取决于错误的原因。

下面是一个可能的蓝色屏幕的一个示例：

![bug 检查示例 windows 10 蓝屏，qr 代码](images/bug-check-example-blue-screen-page-fault.png)

停止代码会显示如[**页面\_容错\_IN\_未分页\_区域**](bug-check-0x50--page-fault-in-nonpaged-area.md)。 当可用时，在执行时的代码的模块名称还会显示，如 AcmeVideo.sys。

如果[内核模式转储文件](kernel-mode-dump-files.md)已写入，这将指示也与百分比完成倒计时转储是在编写。

十六进制值与每个停止的代码如下所示停止代码[Bug 检查代码参考](bug-check-code-reference2.md)。

## <span id="ddk_blue_screen_data_dbg"></span><span id="DDK_BLUE_SCREEN_DATA_DBG"></span>


### <a name="span-idgatheringthestopcodeparametersspanspan-idgatheringthestopcodeparametersspanspan-idgatheringthestopcodeparametersspangathering-the-stop-code-parameters"></a><span id="Gathering_the_Stop_Code_Parameters"></span><span id="gathering_the_stop_code_parameters"></span><span id="GATHERING_THE_STOP_CODE_PARAMETERS"></span>收集停止代码参数

每个错误检查代码具有四个关联的参数提供的其他信息。 参数，请参阅[Bug 检查代码参考](bug-check-code-reference2.md)为每个停止代码。

有多种方法来收集的四个停止代码参数。

-   检查 Windows 系统日志，事件查看器中。 检测的错误的事件属性将列出的四个停止代码参数。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。

-   加载生成的转储文件，并使用[ **！ 分析**](-analyze.md)附有调试器命令。 有关详细信息，请参阅[分析具有 WinDbg 的内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)。

-   将内核调试程序附加到出错的 PC。 停止代码时，调试器输出包含四个参数后停止代码十六进制值。

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

### <a name="span-idbugchecksymbolicnamesspanspan-idbugchecksymbolicnamesspanbug-check-symbolic-names"></a><span id="bug_check_symbolic_names"></span><span id="BUG_CHECK_SYMBOLIC_NAMES"></span>Bug 检查符号名称

[**驱动程序\_电源\_状态\_失败**](bug-check-0x9f--driver-power-state-failure.md)是 Bug 检查符号名称，其中 9F 关联的 bug 检查代码。 停止代码 Bug 检查符号名称与相关联的十六进制值被列入[Bug 检查代码参考](bug-check-code-reference2.md)。

### <a name="span-idreadingbugcheckinformationfromthedebuggerspanspan-idreadingbugcheckinformationfromthedebuggerspanreading-bug-check-information-from-the-debugger"></a><span id="reading_bug_check_information_from_the_debugger"></span><span id="READING_BUG_CHECK_INFORMATION_FROM_THE_DEBUGGER"></span>读取在调试器中的 Bug 检查信息

如果附加一个调试器，bug 检查将导致在目标计算机进入调试器。 在这种情况下，蓝色的屏幕，可能不会立即显示此故障的完整详细信息将发送到调试器并显示在调试器窗口中。 若要查看此信息的第二个时间，请使用[ **.bugcheck （显示 Bug 检查数据）** ](-bugcheck--display-bug-check-data-.md)命令或[ **！ 分析**](-analyze.md)扩展命令.

**内核调试和崩溃转储分析**

内核调试时，尤其是其他故障排除方法失败，或经常发生的问题。 请记住要捕获的错误消息错误检查信息部分中的确切文本。 若要解决复杂问题并开发一种可行的解决方法，它可用于录制会导致失败的确切操作。

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。

有关详细信息，请参阅以下主题：

[使用 Windows 调试器 (WinDbg) 进行故障转储分析](crash-dump-files.md)

[使用 WinDbg 分析内核模式转储文件](analyzing-a-kernel-mode-dump-file-with-windbg.md)

[使用 ！ 分析扩展](using-the--analyze-extension.md)和[！ 分析](-analyze.md)

碎片整理工具显示在第 9 频道- <https://channel9.msdn.com/Shows/Defrag-Tools>

### <a name="span-idusingdriververifiertogatherinformationspanspan-idusingdriververifiertogatherinformationspanspan-idusingdriververifiertogatherinformationspanusing-driver-verifier-to-gather-information"></a><span id="Using_Driver_Verifier_to_Gather_Information"></span><span id="using_driver_verifier_to_gather_information"></span><span id="USING_DRIVER_VERIFIER_TO_GATHER_INFORMATION"></span>使用驱动程序验证程序来收集信息

估计的蓝屏大约三个季度内由错误的驱动程序导致。 驱动程序验证程序是一种工具，运行实时检查驱动程序的行为。 例如，驱动程序验证工具将检查内存资源，如内存池的使用。 如果它看到错误的驱动程序代码执行过程中，它会主动创建例外以允许驱动程序代码以进行进一步仔细检查该部分。 驱动程序验证程序管理器内置于 Windows，可在所有 Windows Pc 上。 若要启动驱动程序验证程序管理器，请键入*Verifier*在命令提示符。 可以配置你想要验证的驱动程序。 验证驱动程序的代码将添加开销在运行，因此请尝试并验证尽可能最少数量的驱动程序。 有关详细信息，请参阅[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。

## <a name="span-idtipsforsoftwareengineersspanspan-idtipsforsoftwareengineersspanspan-idtipsforsoftwareengineersspantips-for-software-engineers"></a><span id="Tips_for_Software_Engineers"></span><span id="tips_for_software_engineers"></span><span id="TIPS_FOR_SOFTWARE_ENGINEERS"></span>软件工程师的提示


由于已编写的代码的 bug 检查时，应使用内核调试程序来分析此问题，然后在代码中修复的错误。 有关完整详细信息，请参阅签入代码的单个 bug [Bug 检查代码参考](bug-check-code-reference2.md)部分。

但是，您可能会遇到不由您自己的代码导致的 bug 检查。 在这种情况下，您可能将不能修复此问题的实际原因，因此，你的目标应该是解决此问题，如有可能隔离并删除有故障的硬件或软件组件。

可以通过基本的故障排除过程，如验证说明、 重新安装关键组件，并验证文件日期解决许多问题。 此外，事件查看器、 Sysinternals 诊断工具和网络监视工具可能会找出并解决这些问题。

有关一般故障排除 Windows bug 检查代码，请按照以下建议：

-   如果你最近添加到系统中，请尝试删除或替换它的硬件。 或者，请与制造商联系，以了解是否有任何修补程序。

-   如果最近，添加新设备驱动程序或系统服务尝试删除或更新它们。 尝试确定导致新的错误检查代码才会显示在系统中更改的内容。

-   查找范围**设备管理器**若要查看的任何设备都带有感叹号 （！）。 查看任何错误的驱动程序的驱动程序属性中显示的事件日志。 请尝试更新相关的驱动程序。

-   检查事件查看器中的系统日志可能会帮助找出设备或导致错误的驱动程序的其他错误消息。 有关详细信息，请参阅[打开事件查看器](https://windows.microsoft.com/windows/what-information-event-logs-event-viewer#1TC=windows-7)。 查找为蓝色的屏幕的同一时间范围内发生在系统日志中的关键错误。

-   您可以尝试运行硬件诊断程序提供的系统制造商。

-   运行 Windows 内存诊断工具，用于测试的内存。 在控件面板的搜索框中，键入内存，然后单击**诊断您的计算机的内存问题**。在测试运行后，使用事件查看器查看系统日志下的结果。 寻找*MemoryDiagnostics 结果*条目以查看结果。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   运行病毒检测程序。 病毒可能会感染所有类型的 for Windows，格式化的硬盘，并生成磁盘损坏可生成系统 bug 检查代码。 请确保病毒检测程序会检查存在感染主启动记录。

-   使用扫描磁盘实用程序以确认没有任何文件系统错误。 右键单击你想要扫描，并选择在驱动器上**属性**。 单击**工具**。 单击**立即检查**按钮。
-   使用系统文件检查器工具来修复丢失或损坏系统文件。 系统文件检查器是一个实用程序允许用户在 Windows 系统文件损坏扫描和还原 Windows 中的损坏的文件。 使用以下命令运行系统文件检查器 (SFC.exe)。

    ```console
    SFC /scannow
    ```

    有关详细信息，请参阅[使用的系统文件检查器工具来修复丢失或损坏系统文件](https://support.microsoft.com/kb/929833)。

-   确认在硬盘上没有足够的可用空间。 操作系统和某些应用程序需要足够的可用空间来创建交换文件和其他功能。 根据系统配置，具体要求各不相同，但它通常是最好有可用的 10%到 15%可用空间。

-   验证系统安装了最新 Service Pack。 若要检测的 Service Pack，如果任何，安装在您的系统上，单击**启动**，单击**运行**，类型**winver**，然后按 ENTER。 **有关 Windows**对话框中显示 Windows 版本号和版本号的 Service Pack，如果安装一个。

-   请与制造商联系，以查看更新的系统 BIOS 或固件是否可用。

-   禁用 BIOS 内存选项，例如缓存或隐藏。

-   对于 Pc，请确保所有扩展板都已正确安装和完全连接所有电缆。

**使用安全模式**

请考虑使用安全模式下时删除或禁用组件。 使用安全模式下加载的最小所需的驱动程序和系统服务在 Windows 启动过程。 若要进入安全模式下，使用**更新和安全**设置中。 选择**恢复**-&gt;**高级启动**启动到维护模式。 在生成菜单中选择**进行故障排除**- &gt; **高级选项** - &gt; **启动设置** - &gt; **重新启动**。 Windows 重新启动到后**启动设置**屏幕上，选择选项 4、 5 或 6 到安全模式下启动。

安全模式下可通过按功能键上启动，例如 F8。 请参阅信息从制造商为特定的启动选项。

## <a name="span-idforcedkebugcheckspanspan-idforcedkebugcheckspanspan-idforcedkebugcheckspanforced-kebugcheck"></a><span id="Forced_KeBugCheck"></span><span id="forced_kebugcheck"></span><span id="FORCED_KEBUGCHECK"></span>强制的 KeBugCheck


若要有意从内核模式驱动程序导致的 bug 检查，需要检查错误的符号将名称传递给**KeBugCheck**或**KeBugCheckEx**函数。 这仅应在没有其他选择是可用的情况下完成。 有关这些函数的更多详细信息，请参阅 Windows 驱动程序工具包。

 

 





