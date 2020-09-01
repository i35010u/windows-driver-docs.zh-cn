---
title: 流类调试
description: 流类调试
ms.assetid: 544b922b-58e4-4cbb-a76c-d8e13ae17e55
keywords:
- Stream.sys 类驱动程序 WDK Windows 2000 内核，调试
- 流式处理微型驱动程序 WDK Windows 2000 内核，调试
- 微型驱动程序 WDK Windows 2000 内核流式处理，调试
- 调试 stream 类微型驱动程序 WDK Windows 2000 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 058ba3e6df9805eb16720316a3cfdecd1f13afc8
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186273"
---
# <a name="stream-class-debugging"></a>流类调试





当遇到微型驱动程序中的错误时，使用选中的 " *stream.sys* 的 (调试") 版本来打印有关微型驱动程序和 ASSERT 状态的信息性消息。

下面是调试 stream 类微型驱动程序时可以使用的其他提示：

-   使用 wdeb386 调试器进行调试时 (或在 Windows Me 系统上使用 Softice) ，调试信息可通过中断到调试器中，键入。NTKERN，然后选择 "选项 D"。此时将显示 "调试日志"，其中按时间顺序显示项。 当通过 Windows 2000 进行调试时，调试信息将实时打印到调试终端。

-   若要调整调试器的输出级别，请加载 *stream.sys* 符号 (windows Me 的 *符号* 和 windows) 2000 的 *stream.sys* ，并将 *StreamDebug* 变量修改为 "e StreamDebug *xx*"。 默认值为00，这会仅打印严重错误。 将其设置为 FF 可打印所有消息。

-   微型驱动程序可以通过调用[**StreamClassDebugPrint**](/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdebugprint)来打印自己的消息，使用之前介绍的*stream.sys*工具。 请注意，前面所述的输出级别必须设置为大于或等于在调用中选择的输出级别。

 

