---
title: 将输出发送到调试器
description: 将输出发送到调试器
keywords:
- 将输出发送到调试器
- OutputDebugString 函数
- DbgPrint 函数
- DbgPrintEx 函数
- KdPrint 函数
- KdPrintEx 函数
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 9971ccd387b789f5cfd114c8b6b0a432d70b51a5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824653"
---
# <a name="sending-output-to-the-debugger"></a>将输出发送到调试器

用户模式和内核模式代码使用不同的例程将输出发送到调试器。

## <a name="user-mode-output-routines"></a>User-Mode 输出例程

**OutputDebugString** 例程将以 null 结尾的字符串发送到调用进程的调试器。 在用户模式驱动程序中， **OutputDebugString** 在调试器命令窗口中显示字符串。 如果调试器未运行，则此例程不起作用。 **OutputDebugString** 不支持 **printf** 格式字符串的变量参数。

此例程的原型如下所示：

```cpp
VOID OutputDebugString(
   LPCTSTR lpOutputString
   );
```

有关此例程的完整文档，请参阅 [与调试器通信](/windows/win32/debug/communicating-with-the-debugger)。

### <a name="kernel-mode-output-routines"></a>Kernel-Mode 输出例程

[**DbgPrint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprint)例程显示调试器窗口中的输出。 此例程支持基本 **printf** 格式参数。 只有内核模式驱动程序可以调用 **DbgPrint**。

[**DbgPrintEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-dbgprintex)例程类似于 **DbgPrint**，但它允许您 "标记" 您的消息。 运行调试器时，只能允许发送具有特定标记的消息。 这允许你仅查看你感兴趣的那些消息。 有关详细信息，请参阅 [读取和筛选调试消息](reading-and-filtering-debugging-messages.md)。


在检查的生成环境中编译时， [**KdPrint**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprint) 和 [**KdPrintEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdprintex) 宏分别与 **DbgPrint** 和 **DbgPrintEx** 完全相同。 在免费生成环境中进行编译时，它们不起作用。
