---
title: 处理分类标注
description: 处理分类标注
ms.assetid: 284aeda0-8275-440f-abf4-84a0c61cc4f4
keywords:
- Windows 筛选平台标注驱动程序 WDK，分类标注
- 标注驱动程序 WDK Windows 筛选平台，分类标注
- classifyFn
- 分类标注 WDK Windows 筛选平台
- 分类标注 WDK Windows 筛选平台，大约分类标注
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5c7d973e7099df39b372a64286a043fd191338d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327639"
---
# <a name="processing-classify-callouts"></a>处理分类标注


筛选器引擎将调用一个标注[ *classifyFn* ](https://msdn.microsoft.com/library/windows/hardware/ff544890)标注函数时没有要处理的标注的网络数据。 满足指定筛选器的操作的标注的筛选器的所有筛选条件时，将发生这种情况。 如果这样的筛选器不具有任何筛选条件，筛选器引擎始终调用的标注*classifyFn*标注函数。

筛选器引擎将多个不同的数据项传递到一个标注*classifyFn*标注函数。 这些数据项包含固定的数据值、 元数据值、 网络原始数据、 筛选器信息和任何流上下文。 筛选器引擎将传递到标注的特定数据项目依赖于特定的筛选层，并在其下的条件*classifyFn*调用。 一个*classifyFn*函数可以使用这些数据项目的任意组合来决定其筛选。

实现一个标注*classifyFn*标注函数取决于哪些标注旨在执行操作。 以下部分提供的一些示例标注的更常见的函数：

[使用适用于深度检测标注](using-a-callout-for-deep-inspection.md)

[使用适用于 Stream 数据的深度检测标注](using-a-callout-for-deep-inspection-of-stream-data.md)

[检查数据包和 Stream 数据](inspecting-packet-and-stream-data.md)

[修改 Stream 数据](modifying-stream-data.md)

[数据日志记录](data-logging.md)

[将上下文与数据流相关联](associating-context-with-a-data-flow.md)

[处理对以异步方式进行分类的标注](processing-classify-callouts-asynchronously.md)

[使用绑定或连接重定向](using-bind-or-connect-redirection.md)

[ALE 终结点生存期管理](ale-endpoint-lifetime-management.md)

[使用数据包标记](using-packet-tagging.md)

一个特定的标注的实际实现*classifyFn*标注函数可以基于这些示例的组合。

对于标注处理筛选的数据层的支持数据流，标注*classifyFn*标注函数可以将上下文关联与每个数据流。 *ClassifyFn*函数可以使用此上下文来保存下次调用由该数据流的筛选器引擎的状态信息。 有关如何标注函数可与数据流关联上下文的详细信息，请参阅[与数据流相关联的上下文](associating-context-with-a-data-flow.md)。

WFP 支持异步处理*classifyFn*标注函数。 有关异步处理的详细信息，请参阅[异步处理分类的标注](processing-classify-callouts-asynchronously.md)。

 

 





