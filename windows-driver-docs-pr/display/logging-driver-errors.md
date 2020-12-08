---
title: 记录驱动程序错误
description: 记录驱动程序错误
keywords:
- 错误日志 WDK 显示
- 错误 WDK 显示
- 记录错误 WDK 显示
ms.date: 10/27/2020
ms.localizationpriority: medium
ms.openlocfilehash: e6a9e1bdb5a64acbf038dcbfbefef77396f8b198
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796237"
---
# <a name="logging-driver-errors"></a>记录驱动程序错误

Microsoft DirectX graphics 内核子系统 (*Dxgkrnl.sys*) 记录将与驱动程序相关的错误、断言、警告和事件显示到内部使用的日志 (*Watchdog.sys*) 。

除了将信息记录到日志之外，默认情况下，如果出现错误或断言，DirectX 图形内核子系统的已检查内部版本将中断到附加的调试器。 默认情况下，DirectX 图形内核子系统的免费内部版本仅将错误和断言记录到日志中，如果出现错误或断言，则不会中断调试器。 你可以通过在注册表中首先创建以下 REG_DWORD 项来更改此默认行为：

```registry
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Logging\BreakOnAssertion
HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Watchdog\Logging\BreakOnError
```

若要使调试器在发生错误或断言时启动，应分别将 **BreakOnError** 或 **BreakOnAssertion** 的值设置为 1 (TRUE) 。 若要使调试器在发生错误或断言时不启动，应分别将 **BreakOnError** 或 **BreakOnAssertion** 的值设置为 0 (FALSE) 。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。
