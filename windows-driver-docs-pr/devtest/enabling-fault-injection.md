---
title: 启用错误注入
description: 启用错误注入
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ea8a8e6cf3a505591c42f3803ac4a9bb8612d79c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819763"
---
# <a name="enabling-fault-injection"></a>启用错误注入


WdfTester 工具提供了一个 WMI 接口，用于为特定驱动程序配置 DDI 错误注入。 提供了一个 (.wsf) 的脚本，该脚本使用此 WMI 接口来配置错误注入。 你可以编写自己的脚本，也可以使用提供的脚本来启用错误注入。 你可以在命令提示符窗口中运行 (.wsf) 的脚本来注册、配置和注销驱动程序。 该脚本还具有一个名为 **runtest** 的命令行选项。

### <a name="span-idwhat_the_runtest_option_doesspanspan-idwhat_the_runtest_option_doesspanwhat-the-runtest-option-does"></a><span id="what_the_runtest_option_does"></span><span id="WHAT_THE_RUNTEST_OPTION_DOES"></span>Runtest 选项的作用

**Runtest** 选项对驱动程序执行简单的禁用和启用操作。 此选项演示如何使用该工具。 首先，该脚本将禁用指定的驱动程序，然后启用该驱动程序。 这允许 WdfTester 监视在禁用和启用操作期间进行的所有 DDI 调用。 此脚本使用 WMI 接口之一来获取在此期间调用的 DDIs 的列表。 该脚本确定哪些 DDIs 可能失败 (仅返回 NTSTATUS) 的。 然后，该脚本调用另一个 WMI 接口来配置 WdfTester，以使列表中的第一个 DDI 失败。 此脚本将禁用并启用驱动程序，这会导致 DDI 失败并触发 WMI 事件。 此脚本已在等待 DDI 的 WMI fail 事件。 如果成功接收事件，并且失败导致计算机无法响应，或导致 bug 检查 (由驱动程序开发人员或测试人员确定) 测试被视为成功。 然后，该脚本会针对列表中的下一个 DDI 重复这些步骤。

**注意**  **Runtest** 选项要求你复制 [DevCon](devcon.md) ( # A0) 工具并将其放在与其他 Wdftester 文件相同的目录中。 Devcon.exe 应用程序位于 *% WDKRoot%* \\ 工具 \\ *&lt; 平台 &gt;* 目录中。

 

**Runtest 选项：**

1.  向 WdfTester 注册驱动程序。 如果你尚未安装驱动程序，则必须先安装它，然后才能使用 runtest。

2.  在运行 Windows Vista 或更高版本 (计算机上启用此驱动程序的驱动程序验证程序不需要重启) 。

3.  使用 Devcon 应用程序禁用该驱动程序。

4.  使用 Devcon 应用程序启用驱动程序。

5.  检索在启用和禁用操作期间调用的函数的名称，并标识返回 NTSTATUS 并可能失败的函数。

6.  启动异步 WMI 事件通知。

7.  对于第5步中获取的列表，可能会失败的每个 DDI：
    1.  为失败配置函数。
    2.  使用 Devcon.exe 禁用然后启用驱动程序。 此操作调用函数，并且 WdfTester 无法调用函数。
    3.  等待触发 WMI 事件。
    4.  如果触发了 WMI 事件，则 **runtest** 选项会对列表中的下一个函数重复步骤7。

8.  注销驱动程序。

 

 





