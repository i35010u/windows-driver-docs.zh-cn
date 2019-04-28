---
title: 解释 Bug 检查代码
description: 当 Microsoft Windows 遇到一个条件，从而危及安全系统的状态时，系统就会停止。
ms.assetid: b5c8e18e-c2d3-47d9-b2bd-38aaaedcfde9
keywords:
- 工具 WDK，bug 检查代码
- 驱动程序开发工具 WDK，bug 检查代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ad601c2da8e67a4ae181e9f03e7bc2adad2ebf4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340477"
---
# <a name="interpreting-a-bug-check-code"></a>解释 Bug 检查代码


当 Microsoft Windows 遇到一个条件，从而危及安全系统的状态时，系统就会停止。 这种情况称为*bug 检查*。 它通常也称为*系统崩溃*即*内核错误*即*停止错误*，或*BSOD*。 硬件设备、 其驱动程序或相关的软件可能会导致此错误。

如果在系统上启用了故障转储，创建的崩溃转储文件。

如果内核调试器已附加并处于活动状态，系统会导致中断，可以使用调试器来调查在发生崩溃。

如果未附加调试器，蓝色文本屏幕会显示有关错误的信息。 调用此屏幕*蓝屏*、 一个*错误检查屏幕*即*停止屏幕*，或*BSOD*。

## <span id="ddk_interpreting_bug_check_codes_tools"></span><span id="DDK_INTERPRETING_BUG_CHECK_CODES_TOOLS"></span>


错误检查屏幕的确切外观取决于错误的原因。 下面是一个可能的 bug 检查屏幕的一个示例：

```
STOP: 0x00000079 (0x00000002, 0x00000001, 0x00000002, 0x00000000)

Mismatched kernel and hal image.

Beginning dump of physical memory
Physical memory dump complete. Contact your system administrator or
technical support group.
```

但是，一些蓝色屏幕如下所示：

```
STOP: c000021a {Fatal System Error}

The Windows Logon Process system process terminated unexpectedly with
a status of 0x00000001 (0x00000000 0x00000000).
The system has been shut down.
```

### <span id="ddk_blue_screen_data_tools"></span><span id="DDK_BLUE_SCREEN_DATA_TOOLS"></span>

名为"STOP"一词的十六进制数*bug 检查代码*或*停止代码*。 这是在屏幕上最重要的项。

每个错误检查代码具有四个关联的参数。 在第一个蓝色屏幕如下所示，所有四个参数将显示后错误检查代码。 但是，在蓝色屏幕的第二个类型，这些参数排列中的说明性文本。 重新排列的量，无论它们将始终按顺序显示。 如果出现少于四个参数，可以假定剩余参数为零。

在蓝色屏幕上文本的其余部分提供了其他信息。 对于某些错误检查的执行，这可能是发生了什么情况或建议以便进行如何处理该问题的说明。 如果已编写一个内核模式转储文件，这通常将还指示。

在某些情况下，Windows 将显示在蓝色屏幕中的，仅第一行。 如果显示所需的重要服务已受此错误，这可能发生。

### <a name="span-idbugchecksymbolicnamesspanspan-idbugchecksymbolicnamesspanbug-check-symbolic-names"></a><span id="bug_check_symbolic_names"></span><span id="BUG_CHECK_SYMBOLIC_NAMES"></span>Bug 检查符号名称

每个 bug 检查代码也有关联的符号名称。 在蓝色屏幕上通常不显示这些名称。 在这些示例中，显示的第一个屏幕[ **bug 检查 0x79** ](https://msdn.microsoft.com/library/windows/hardware/ff559209) (不匹配\_HAL)，而第二部分演示[ **bug 检查 0xC000021A**](https://msdn.microsoft.com/library/windows/hardware/ff560177) (状态\_系统\_进程\_已终止)。

您可以故意导致的 bug 检查从内核模式驱动程序的 bug 检查符号将名称传递给[ **KeBugCheck** ](https://msdn.microsoft.com/library/windows/hardware/ff551948)或[ **KeBugCheckEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551961). 这仅应在没有其他选择是可用的情况下完成。

### <a name="span-idreadingbugcheckinformationfromthedebuggerspanspan-idreadingbugcheckinformationfromthedebuggerspanreading-bug-check-information-from-the-debugger"></a><span id="reading_bug_check_information_from_the_debugger"></span><span id="READING_BUG_CHECK_INFORMATION_FROM_THE_DEBUGGER"></span>读取在调试器中的 Bug 检查信息

如果附加一个调试器，bug 检查将导致在目标计算机进入调试器。 在这种情况下，蓝色的屏幕，可能不会显示，或可能会显示具有较少文本;此故障的完整详细信息将发送到调试器，在调试器窗口中显示。 有关详细信息，请参阅[使用调试器](using-a-debugger.md)。

可以作为的一部分找到的 bug 检查代码本参考部分[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)。 请参阅[Bug 检查代码参考](https://msdn.microsoft.com/library/windows/hardware/hh994433)有关的错误检查的执行和参数的说明。 每个引用页列出了错误检查代码、 文本字符串和四个其他参数显示的与每个 bug 检查。 它还介绍如何诊断错误导致的错误检查和处理错误的可能方法。

Bug 的完整列表检查代码，请参阅 Bugcodes.h 文件。 可以在 inc 目录的 Microsoft Windows Driver Kit (WDK) 中找到此文件。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[Bug 检查代码参考](https://msdn.microsoft.com/library/windows/hardware/hh994433)

[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)

 

 






