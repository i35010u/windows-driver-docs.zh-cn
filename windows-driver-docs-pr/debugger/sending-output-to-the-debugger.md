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
ms.openlocfilehash: f36b17bc543213ccb01cb8f985d4be42e8086b5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381980"
---
# <a name="sending-output-to-the-debugger"></a>将输出发送到调试器


## <span id="ddk_sending_output_to_the_debugger_dbg"></span><span id="DDK_SENDING_OUTPUT_TO_THE_DEBUGGER_DBG"></span>


用户模式和内核模式代码使用不同的例程将输出发送到调试器。

### <a name="span-idusermodeoutputroutinesspanspan-idusermodeoutputroutinesspanuser-mode-output-routines"></a><span id="user_mode_output_routines"></span><span id="USER_MODE_OUTPUT_ROUTINES"></span>用户模式下输出例程

**OutputDebugString**将以 null 结尾的字符串发送到调用进程的调试器。 在用户模式驱动程序， **OutputDebugString**调试器命令窗口中显示的字符串。 如果调试器未运行，则此例程无效。 **OutputDebugString**不支持的变量自变量**printf**格式的字符串。

此例程的完整文档，请参阅 Microsoft Windows SDK。

### <a name="span-idkernelmodeoutputroutinesspanspan-idkernelmodeoutputroutinesspankernel-mode-output-routines"></a><span id="kernel_mode_output_routines"></span><span id="KERNEL_MODE_OUTPUT_ROUTINES"></span>内核模式输出例程

**DbgPrint**调试器窗口中显示输出。 此例程支持 basic **printf**设置参数的格式。 仅内核模式代码可以调用**DbgPrint**。

**DbgPrintEx**类似于**DbgPrint**，但它允许您以"标记"消息。 当运行调试器，可以允许仅这些具有某些标记要发送的消息。 这样，您可以查看你感兴趣的那些消息。 有关详细信息，请参阅[读取和筛选调试消息](reading-and-filtering-debugging-messages.md)。

**请注意**  在 Windows Vista 和更高版本的 Windows， **DbgPrint**生成标记的消息以及。 这是从早期版本 Windows 的更改。

 

**KdPrint**和**KdPrintEx**等于**DbgPrint**并**DbgPrintEx**分别在已检验的版本环境中编译时。 编译时可用的生成环境中，它们会产生任何影响。

这些例程，以及生成环境的完整文档，请参阅 Windows 驱动程序工具包。

 

 





