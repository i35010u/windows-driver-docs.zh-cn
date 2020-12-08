---
title: 解释 Bug 检查代码
description: 当 Microsoft Windows 遇到损害安全系统操作的情况时，系统将会挂起。
keywords:
- 工具 WDK，bug 检查代码
- 驱动程序开发工具 WDK，bug 检查代码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417fa77f88a03bd72f472f355c284f5f3b91c08e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813861"
---
# <a name="interpreting-a-bug-check-code"></a>解释 Bug 检查代码

当 Microsoft Windows 遇到损害安全系统操作的情况时，系统将会挂起。 此条件称为 " *bug 检查*"。 通常也称为 *系统崩溃*、 *内核错误*、 *停止错误* 或 *BSOD*。 硬件设备、其驱动程序或相关软件可能导致此错误。

如果系统上启用了故障转储，则会创建故障转储文件。

如果内核调试器已附加并且处于活动状态，则系统会导致中断，因此可以使用调试器来调查故障。

如果未附加调试器，则会出现蓝色文本屏幕，其中包含有关错误的信息。 此屏幕称为 *蓝屏*、 *bug 检查屏幕*、 *停止屏幕* 或 *BSOD*。

## <a name="interpreting-bug-check-code-tools"></a>解释 bug 检查代码工具

Bug 检查屏幕的确切外观取决于错误的原因。 下面是一个可能的错误检查屏幕的示例：

```cmd
STOP: 0x00000079 (0x00000002, 0x00000001, 0x00000002, 0x00000000)

Mismatched kernel and hal image.

Beginning dump of physical memory
Physical memory dump complete. Contact your system administrator or
technical support group.
```

另一方面，某些蓝色屏幕如下所示：

```cmd
STOP: c000021a {Fatal System Error}

The Windows Logon Process system process terminated unexpectedly with
a status of 0x00000001 (0x00000000 0x00000000).
The system has been shut down.
```

### <a name="data-tools"></a>数据工具

单词 "STOP" 后的十六进制数称为 *bug 检查代码* 或 *停止代码*。 这是屏幕上最重要的项。

每个 bug 检查代码都有四个关联参数。 在此处显示的第一个蓝屏中，所有四个参数都显示在 bug 检查代码之后。 但是，在第二种蓝屏中，这些参数已在说明文本中重新排列。 不管重新排列量如何，它们始终会按顺序显示。 如果显示的参数少于四个，则其余的参数可假定为零。

蓝色屏幕上的其余文本将提供其他信息。 对于某些 bug 检查，这可能是对发生了什么问题的说明，或者是有关如何处理问题的建议。 如果已写入内核模式转储文件，则该文件通常也会指明。

在某些情况下，Windows 只显示蓝屏的第一行。 如果显示所需的关键服务已受错误影响，则会发生这种情况。

### <a name="bug-check-symbolic-names"></a>Bug 检查符号名称

每个 bug 检查代码还具有关联的符号名称。 这些名称通常不会出现在蓝色屏幕上。 在这些示例中，第一个屏幕显示 [**bug 检查 0x79**](../debugger/bug-check-0x79--mismatched-hal.md) (不匹配 \_ 的 HAL) ，第二个屏幕显示 [**BUG 检查 0xc000021a**](../debugger/bug-check-0xc000021a--winlogin-fatal-error.md) (状态 \_ 系统 \_ 进程已 \_ 终止) 。

您可以通过将 bug 检查的符号名称传递给 [**KeBugCheck**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-kebugcheck) 或 [**KeBugCheckEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kebugcheckex)，从内核模式驱动程序中有意地引发 bug 检查。 只有在没有其他选项可用的情况下，才应执行此操作。

### <a name="reading-bug-check-information-from-the-debugger"></a>从调试器读取 Bug 检查信息

如果附加了调试器，则 bug 检查将导致目标计算机中断到调试器。 在这种情况下，可能不会显示蓝色屏幕，也可能显示较少文本;此崩溃的完整详细信息将发送到调试器，并显示在调试器窗口中。 有关详细信息，请参阅 [使用调试器](using-a-debugger.md)。

可在 [Windows 调试](../debugger/index.md)过程中找到 bug 检查代码的此参考部分。 有关 bug 检查和参数的说明，请参阅 [Bug 检查代码引用](../debugger/bug-check-code-reference2.md) 。 每个引用页面都列出了 bug 检查代码、文本字符串和与每个 bug 检查一起显示的四个附加参数。 还介绍了如何诊断导致错误检查的错误，以及处理错误的可能方法。

有关 bug 检查代码的完整列表，请参阅 Bugcodes 文件。 此文件可以在 Microsoft Windows 驱动程序工具包 (WDK) 中找到。

## <a name="related-topics"></a>相关主题

[Bug 检查代码参考](../debugger/bug-check-code-reference2.md)

[Windows 调试](../debugger/index.md)
