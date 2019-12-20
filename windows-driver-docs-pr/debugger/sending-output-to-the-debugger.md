---
title: 将输出发送到调试器
description: 将输出发送到调试器
ms.assetid: e0640e70-9846-4239-a3ff-b78788751384
keywords:
- 将输出发送到调试器
- OutputDebugString 函数
- DbgPrint 函数
- DbgPrintEx 函数
- KdPrint 函数
- KdPrintEx 函数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0aa10a13187565ff7cedf9e407a58b3e7a0aa80
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209789"
---
# <a name="sending-output-to-the-debugger"></a>将输出发送到调试器


## <span id="ddk_sending_output_to_the_debugger_dbg"></span><span id="DDK_SENDING_OUTPUT_TO_THE_DEBUGGER_DBG"></span>


用户模式和内核模式代码使用不同的例程将输出发送到调试器。

### <a name="span-iduser_mode_output_routinesspanspan-iduser_mode_output_routinesspanuser-mode-output-routines"></a><span id="user_mode_output_routines"></span><span id="USER_MODE_OUTPUT_ROUTINES"></span>用户模式输出例程

**OutputDebugString**将以 null 结尾的字符串发送到调用进程的调试器。 在用户模式驱动程序中， **OutputDebugString**在调试器命令窗口中显示字符串。 如果调试器未运行，则此例程不起作用。 **OutputDebugString**不支持**printf**格式字符串的变量参数。

有关此例程的完整文档，请参阅 Microsoft Windows SDK。

### <a name="span-idkernel_mode_output_routinesspanspan-idkernel_mode_output_routinesspankernel-mode-output-routines"></a><span id="kernel_mode_output_routines"></span><span id="KERNEL_MODE_OUTPUT_ROUTINES"></span>内核模式输出例程

**DbgPrint**在调试器窗口中显示输出。 此例程支持基本**printf**格式参数。 只有内核模式代码可以调用**DbgPrint**。

**DbgPrintEx**类似于**DbgPrint**，但它允许你 "标记" 你的消息。 运行调试器时，只能允许发送具有特定标记的消息。 这允许你仅查看你感兴趣的那些消息。 有关详细信息，请参阅[读取和筛选调试消息](reading-and-filtering-debugging-messages.md)。

**请注意**，在 windows Vista 和更高版本的 windows 中  ， **DbgPrint**也会生成标记的消息。 这是对以前版本的 Windows 的一项更改。
在已检查的生成环境中编译时， **KdPrint**和**KdPrintEx**分别与**DbgPrint**和**DbgPrintEx**相同。 在免费生成环境中进行编译时，它们不起作用。

有关这些例程以及生成环境的完整文档，请参阅 Windows 驱动程序工具包。
