---
title: Stream 类调试
description: Stream 类调试
ms.assetid: 544b922b-58e4-4cbb-a76c-d8e13ae17e55
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，调试
- 流式处理微型驱动程序 WDK Windows 2000 内核调试
- 微型驱动程序 WDK Windows 2000 内核流式处理，调试
- 调试流类微型驱动程序 WDK Windows 2000 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2afff5ab5c84684411417be7acaf3d8aa2e0dd47
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527014"
---
# <a name="stream-class-debugging"></a>Stream 类调试





使用选中 （调试） 版本的*stream.sys*遇到微型驱动程序中的错误时打印出有关断言的微型驱动程序的状态信息性消息。

调试流类微型驱动程序时，可以使用以下、 其他提示：

-   在 Windows Me 的系统上调试使用 wdeb386 调试器 （或使用 Softice），调试信息将可通过中断到调试器中，键入。NTKERN，，然后选择选项 d。这将显示调试日志，按时间顺序显示的条目。 在调试时与 Windows 2000，调试信息打印到终端实时调试。

-   若要调整调试器的输出级，加载*stream.sys*符号 (*stream.sym* Windows 我和*stream.sys*适用于 Windows 2000) 和修改*StreamDebug*变量与"e StreamDebug *xx*"。 默认值为 00，这将输出仅为严重错误。 将其设置为 FF 要打印的所有消息。

-   微型驱动程序可以打印自己的消息，使用*stream.sys*设施前面所述，通过调用[ **StreamClassDebugPrint**](https://msdn.microsoft.com/library/windows/hardware/ff568235)。 请注意，如前面所述的输出级别必须设置为大于或等于所选的调用中的输出级别。

 

 




