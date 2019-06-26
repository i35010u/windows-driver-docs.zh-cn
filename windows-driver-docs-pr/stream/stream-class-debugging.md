---
title: 流类调试
description: 流类调试
ms.assetid: 544b922b-58e4-4cbb-a76c-d8e13ae17e55
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，调试
- 流式处理微型驱动程序 WDK Windows 2000 内核调试
- 微型驱动程序 WDK Windows 2000 内核流式处理，调试
- 调试流类微型驱动程序 WDK Windows 2000 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 060ddb9dc4cd370fed1bfa2361c9ee909679a5ba
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377815"
---
# <a name="stream-class-debugging"></a>流类调试





使用选中 （调试） 版本的*stream.sys*遇到微型驱动程序中的错误时打印出有关断言的微型驱动程序的状态信息性消息。

调试流类微型驱动程序时，可以使用以下、 其他提示：

-   在 Windows Me 的系统上调试使用 wdeb386 调试器 （或使用 Softice），调试信息将可通过中断到调试器中，键入。NTKERN，，然后选择选项 d。这将显示调试日志，按时间顺序显示的条目。 在调试时与 Windows 2000，调试信息打印到终端实时调试。

-   若要调整调试器的输出级，加载*stream.sys*符号 (*stream.sym* Windows 我和*stream.sys*适用于 Windows 2000) 和修改*StreamDebug*变量与"e StreamDebug *xx*"。 默认值为 00，这将输出仅为严重错误。 将其设置为 FF 要打印的所有消息。

-   微型驱动程序可以打印自己的消息，使用*stream.sys*设施前面所述，通过调用[ **StreamClassDebugPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/strmini/nf-strmini-streamclassdebugprint)。 请注意，如前面所述的输出级别必须设置为大于或等于所选的调用中的输出级别。

 

 




