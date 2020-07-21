---
title: 将输出发送到调试器
description: 将输出发送到调试器
ms.assetid: ee167261-78cd-4178-ba98-3250cc735657
keywords:
- 调试代码 WDK，发送输出
- 将输出发送到调试器
- 输出例程 WDK
- 用户模式输出例程 WDK
- 内核模式输出例程 WDK
- 例程调试，输出
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7b0096388d1c43baaafde7532c18737413e523d5
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86568062"
---
# <a name="sending-output-to-the-debugger"></a>将输出发送到调试器

用户模式和内核模式驱动程序使用不同的例程将输出发送到调试器。

## <a name="user-mode-output-routines"></a>用户模式输出例程

**OutputDebugString**例程将以 null 结尾的字符串发送到调用进程的调试器。 在用户模式驱动程序中， **OutputDebugString**在调试器命令窗口中显示字符串。 如果调试器未运行，则此例程不起作用。 **OutputDebugString**不支持**printf**格式字符串的变量参数。

此例程的原型如下所示：

```cpp
VOID OutputDebugString(
   LPCTSTR lpOutputString
   );
```

此例程可由包含 windows .h 标头的任何用户模式驱动程序调用。 有关此例程和其他可用于调试的用户模式例程的完整文档，请参阅 Microsoft Windows SDK。

## <a name="kernel-mode-output-routines"></a>内核模式输出例程

[**DbgPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)例程显示调试器窗口中的输出。 此例程支持基本**printf**格式参数。 只有内核模式驱动程序可以调用**DbgPrint**。

[**DbgPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)例程类似于**DbgPrint**，但它允许您 "标记" 您的消息。 运行调试器时，只能允许发送具有特定标记的消息。 这允许你仅查看你感兴趣的那些消息。 有关详细信息，请参阅[读取和筛选调试消息](reading-and-filtering-debugging-messages.md)。

> [!NOTE]
> 在 Windows Vista 和更高版本的 Windows 中， **DbgPrint**也会生成标记的消息。 在以前版本的 Windows 中， **DbgPrint**生成了未标记的消息。

在检查的生成环境中编译时， [**KdPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint)和[**KdPrintEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex)宏分别与**DbgPrint**和**DbgPrintEx**完全相同。 在免费生成环境中进行编译时，它们不起作用。
