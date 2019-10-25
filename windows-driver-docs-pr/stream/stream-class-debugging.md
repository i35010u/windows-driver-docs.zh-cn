---
title: 流类调试
description: 流类调试
ms.assetid: 544b922b-58e4-4cbb-a76c-d8e13ae17e55
keywords:
- Stream .sys 类驱动程序 WDK Windows 2000 内核，调试
- 流式处理微型驱动程序 WDK Windows 2000 内核，调试
- 微型驱动程序 WDK Windows 2000 内核流式处理，调试
- 调试 stream 类微型驱动程序 WDK Windows 2000 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a571acc40cf4474938965184157d0d99db25be6
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837683"
---
# <a name="stream-class-debugging"></a>流类调试





当遇到微型驱动程序中的错误时，请使用 checked （调试）版本的*stream*打印有关微型驱动程序和 ASSERT 状态的信息性消息。

下面是调试 stream 类微型驱动程序时可以使用的其他提示：

-   当使用 wdeb386 调试器（或通过 Softice）在 Windows Me 系统上进行调试时，调试信息可通过中断到调试器中，键入。NTKERN，然后选择 "选项 D"。此时将显示 "调试日志"，其中按时间顺序显示项。 当通过 Windows 2000 进行调试时，调试信息将实时打印到调试终端。

-   若要调整调试器的输出级别，*请加载*符号符号（适用于 windows Me 的 StreamDebug 和用于 windows *2000 的* ），并将变量修改为 "e StreamDebug *xx*"。 默认值为00，这会仅打印严重错误。 将其设置为 FF 可打印所有消息。

-   微型驱动程序可以通过调用[**StreamClassDebugPrint**](https://docs.microsoft.com/windows-hardware/drivers/ddi/strmini/nf-strmini-streamclassdebugprint)来使用前面所述的*sys.databases*功能打印自己的消息。 请注意，前面所述的输出级别必须设置为大于或等于在调用中选择的输出级别。

 

 




