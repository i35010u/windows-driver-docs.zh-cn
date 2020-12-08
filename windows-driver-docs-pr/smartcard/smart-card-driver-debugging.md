---
title: 智能卡驱动程序调试
description: 智能卡驱动程序调试
keywords:
- 智能卡驱动程序 WDK，调试
- 调试驱动程序 WDK 智能卡
- DebugLevel
- 供应商提供的驱动程序 WDK 智能卡，调试
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 26a2b355bd5969b2d9742f8d326ad53fe09217d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804883"
---
# <a name="smart-card-driver-debugging"></a>智能卡驱动程序调试

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。

智能卡驱动程序库支持多种调试功能。 每个调试功能由以下常量之一表示，这些常量是在 *Smclib* 头文件中定义的：

```cpp
DEBUG_IOCTL
DEBUG_ATR
DEBUG_PROTOCOL
DEBUG_DRIVER
DEBUG_TRACE
DEBUG_ERROR
DEBUG_BREAK
DEBUG_ALL
```

启用的调试功能的组合集由一个称为 *调试级别* 的值表示。 您可以通过采用与要启用的功能对应的常量的按位 OR 来计算此值。

可以通过两种方式设置调试级别。 首先，可以使用 Windows 驱动程序工具包附带的智能卡驱动程序测试程序 *Scdrvtst*，)  (。 第二种是使用 [**SmartcardSetDebugLevel**](/previous-versions/ff548960(v=vs.85)) 智能卡驱动程序库例程。

在这两种情况下，必须将所需的调试级别的值传递到设置调试级别的程序或例程。 例如，若要使用智能卡库例程从驱动程序设置调试级别，请执行以下调用：

```cpp
SmartcardSetDebugLevel(DebugLevel);
```

若要从读取器驱动程序写入调试消息，驱动程序必须调用以下例程：

```cpp
SmartcardDebug(
 ULONG DebugLevel,
 PCHAR Message
);
```

> [!IMPORTANT]
> 您必须安装所选版本的操作系统和该驱动程序的已检查版本，才能获取调试消息。

此例程还可用于通过以下方式将消息写入远程调试器。

- 若要编写错误消息，请使用 \_ *DEBUGLEVEL* 的调试错误常量。

- 若要写入标准驱动程序消息，请使用调试 \_ 驱动程序常量。

- 若要编写指示读取器驱动程序何时进入或退出例程的跟踪消息，请使用调试 \_ 跟踪作为 *DebugLevel*。

开发驱动程序时，请使用所选的智能卡驱动程序库版本，并使用 **SmartcardSetDebugLevel** (调试 \_ *DriverEntry* 例程中的所有) 来设置最大调试级别。

有关设置远程调试会话的信息，请参阅 [Windows 调试](../debugger/index.md)。
