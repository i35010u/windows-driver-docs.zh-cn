---
title: NDIS 调试概述
description: NDIS 调试概述
keywords:
- NDIS 调试，概述
ms.date: 05/14/2020
ms.localizationpriority: medium
ms.openlocfilehash: c7d1b495cf03afd343280430e5a0c8004df967dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786967"
---
# <a name="overview-of-ndis-debugging"></a>NDIS 调试概述

调试网络驱动程序的两种主要工具是调试跟踪和网络驱动程序接口规范 (NDIS) 扩展。 有关调试跟踪的详细信息，请参阅 [启用 NDIS 调试跟踪](enabling-ndis-debug-tracing.md)。 有关 NDIS 调试扩展的详细信息，请参阅 [Ndis 扩展](ndis-extensions--ndiskd-dll-.md)，其中提供了在扩展模块 Ndiskd.dll 中找到的扩展命令的完整列表。

使用 netreport 命令生成显示当前适配器和协议的视觉报表 [ndiskd](-ndiskd-netreport.md) 。

![ndiskd. netreport 彩色编码的输出，其中显示了演示多个适配器的两列](images/ndis-report.png)

然后，可以使用 [ndiskd get-netadapter](-ndiskd-netadapter.md) 内核调试器命令来调查当前的驱动程序集。

```dbgconsole
1: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name
    ffffdf8015a98380   ffffdf8015aa11a0    Microsoft ISATAP Adapter #2
    ffffdf801418d650   ffffdf80140c71a0    Microsoft Kernel Debug Network Adapter
```

用于调试网络驱动程序的另一个工具是常规调试扩展的集合，这对获取调试信息非常有用。 例如，输入 [！ stack 2 ndis！](-stacks.md) 显示堆栈中以 **ndis！** 开头的所有线程。 此信息可用于调试挂起和停止。 有关 WinDbg 入门的常规信息，请参阅 [Windows 调试](getting-started-with-windows-debugging.md)入门。

## <a name="driver-verifier"></a>驱动程序验证程序

用于测试 NDIS 驱动程序的另一个有用工具是 "NDIS 验证程序"。 有关详细信息，请参阅 [NDIS 驱动程序](../devtest/sdv-rules-for-ndis-drivers.md) 和 [静态驱动程序验证](../devtest/static-driver-verifier.md)程序的规则。

## <a name="ndis-debugging-resources"></a>NDIS 调试资源

碎片整理工具显示的剧集175介绍 [了 #175 调试网络堆栈的 NDIS 调试碎片整理工具](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)。

Ndis 团队博客存档在 [ndis 博客](/archive/blogs/ndis/)上提供。

## <a name="ndis-bug-checks"></a>NDIS Bug 检查

此外还提供了特定于 NDIS 的 bug 检查代码、bug 检查 0x7C (BUGCODE \_ NDIS \_ 驱动程序) 。 有关参数的完整列表，请参阅 [Bug 检查 0x7C](bug-check-0x7c--bugcode-ndis-driver.md)。

常见的 NDIS misbehavior 相关 bug 检查是 [错误检查0xD1： DRIVER_IRQL_NOT_LESS_OR_EQUAL](bug-check-0xd1--driver-irql-not-less-or-equal.md) 这可能由驱动程序代码本身引起。 这很可能是一个错误或内存损坏，最终会将自身表现为错误指针。

另一个常见问题是 [错误检查0x9F： DRIVER_POWER_STATE_FAILURE](bug-check-0x9f--driver-power-state-failure.md)。

所有 bug 检查的第一步是查找好的转储文件，将其加载到 Windows 调试器中，然后使用 [！ "分析](-analyze.md) " 命令。 有关详细信息，请参阅 [使用！分析扩展](using-the--analyze-extension.md)。
