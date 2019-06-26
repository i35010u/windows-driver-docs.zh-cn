---
title: 将输出发送到调试器
description: 将输出发送到调试器
ms.assetid: ee167261-78cd-4178-ba98-3250cc735657
keywords:
- 调试代码 WDK，将输出发送
- 将输出发送到调试器
- 输出例程 WDK
- 用户模式下输出例程 WDK
- 内核模式输出例程 WDK
- 例程 WDK 调试输出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca4cd449ab950ca82c8a4c9719c076525cc020a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374425"
---
# <a name="sending-output-to-the-debugger"></a>将输出发送到调试器


## <span id="ddk_sending_output_to_the_debugger_tools"></span><span id="DDK_SENDING_OUTPUT_TO_THE_DEBUGGER_TOOLS"></span>


用户模式和内核模式驱动程序使用不同的例程将输出发送到调试器。

### <a name="span-idusermodeoutputroutinesspanspan-idusermodeoutputroutinesspanuser-mode-output-routines"></a><span id="user_mode_output_routines"></span><span id="USER_MODE_OUTPUT_ROUTINES"></span>用户模式下输出例程

**OutputDebugString**例程将以 null 结尾的字符串发送到调用进程的调试器。 在用户模式驱动程序， **OutputDebugString**调试器命令窗口中显示的字符串。 如果调试器未运行，则此例程无效。 **OutputDebugString**不支持的变量自变量**printf**格式的字符串。

此例程的原型如下所示：

```
VOID OutputDebugString(
   LPCTSTR lpOutputString
   );
```

此例程可由任何用户模式驱动程序，它包含 windows.h 标头调用。 此例程和其他用户模式下例程用于调试的完整文档，请参阅 Microsoft Windows SDK。

### <a name="span-idkernelmodeoutputroutinesspanspan-idkernelmodeoutputroutinesspankernel-mode-output-routines"></a><span id="kernel_mode_output_routines"></span><span id="KERNEL_MODE_OUTPUT_ROUTINES"></span>内核模式输出例程

[ **DbgPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprint)例程调试器窗口中显示输出。 此例程支持 basic **printf**设置参数的格式。 只将内核模式驱动程序可以调用**DbgPrint**。

[ **DbgPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-dbgprintex)例程是类似于**DbgPrint**，但它允许您以"标记"消息。 当运行调试器，可以允许仅这些具有某些标记要发送的消息。 这样，您可以查看你感兴趣的那些消息。 有关详细信息，请参阅[读取和筛选调试消息](reading-and-filtering-debugging-messages.md)。

**请注意**  在 Windows Vista 和更高版本的 Windows， **DbgPrint**生成标记的消息以及。 在以前版本的 Windows， **DbgPrint**生成未标记的消息。

 

[ **KdPrint** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprint)并[ **KdPrintEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdprintex)宏相等**DbgPrint**和**DbgPrintEx**分别在已检验的版本环境中编译时。 编译时可用的生成环境中，它们会产生任何影响。

 

 





