---
title: 处理分类标注
description: 处理分类标注
ms.assetid: 284aeda0-8275-440f-abf4-84a0c61cc4f4
keywords:
- Windows 筛选平台标注驱动程序 WDK，分类标注
- 标注驱动程序 WDK Windows 筛选平台，对标注进行分类
- classifyFn
- 对注解 WDK Windows 筛选平台进行分类
- 分类标注 WDK Windows 筛选平台，关于对标注进行分类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3cbf07c444443dc1cde376d4fc117d5f5b513006
ms.sourcegitcommit: 20eac54e419a594f7cea766ee28f158559dfd79c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/06/2020
ms.locfileid: "91754960"
---
# <a name="processing-classify-callouts"></a>处理分类标注


如果有要通过标注处理的网络数据，则筛选器引擎将调用标注的 [*classifyFn*](/windows-hardware/drivers/ddi/fwpsk/nc-fwpsk-fwps_callout_classify_fn0) 标注函数。 对于指定筛选器操作的标注的筛选器，所有筛选条件都为 true，则会发生这种情况。 如果此类筛选器没有筛选条件，则筛选器引擎始终调用标注的 *classifyFn* callout 函数。

筛选器引擎将多个不同的数据项传递给标注的 *classifyFn* callout 函数。 这些数据项包括固定的数据值、元数据值、原始网络数据、筛选器信息和任何流上下文。 筛选器引擎传递给标注的特定数据项取决于特定筛选层和调用 *classifyFn* 的条件。 *ClassifyFn*函数可以使用这些数据项的任意组合来做出筛选决策。

标注的 *classifyFn* callout 函数的实现取决于标注的设计方式。 以下部分提供了一些更典型的标注功能的示例：

[使用标注进行深度检测](using-a-callout-for-deep-inspection.md)

[使用标注进行流数据深度检测](using-a-callout-for-deep-inspection-of-stream-data.md)

[检查数据包和流数据](packet-inspection-points.md)

[修改流数据](modifying-stream-data.md)

[数据日志记录](data-logging.md)

[将上下文与数据流相关联](associating-context-with-a-data-flow.md)

[以异步方式处理分类标注](processing-classify-callouts-asynchronously.md)

[使用绑定或连接重定向](using-bind-or-connect-redirection.md)

[ALE 终结点生存期管理](ale-endpoint-lifetime-management.md)

[使用数据包标记](using-packet-tagging.md)

特定标注的 *classifyFn* 标注函数的实际实现可基于这些示例的组合。

对于在支持数据流的筛选层处理数据的标注，标注的 *classifyFn* callout 函数可以将上下文与每个数据流相关联。 *ClassifyFn*函数可以使用此上下文保存状态信息，以便在该数据流的筛选器引擎下次调用时保存状态信息。 有关 callout 函数如何将上下文与数据流相关联的详细信息，请参阅将 [上下文与](associating-context-with-a-data-flow.md)数据流相关联。

WFP 支持 *classifyFn* 标注函数的异步处理。 有关异步处理的详细信息，请参阅 [异步处理分类标注](processing-classify-callouts-asynchronously.md)。

 

