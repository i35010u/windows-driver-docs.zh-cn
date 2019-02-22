---
title: Directshow 缓存 Pin 信息
description: Directshow 缓存 Pin 信息
ms.assetid: 1e6a973b-32d2-4ac2-9cd6-f4d3c329cecf
keywords:
- pin 数据缓存 WDK BDA
- 缓存 WDK AVStream
- DirectShow pin 数据缓存 WDK AVStream
- 更新 pin 数据缓存 WDK AVStream
- 广播驱动程序体系结构 WDK AVStream，pin 数据缓存
- BDA WDK AVStream，pin 数据缓存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f215ce1a0a39092dc180dc1e5390dd7a5a1a6f7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556180"
---
# <a name="caching-pin-information-for-directshow"></a>Directshow 缓存 Pin 信息





应用程序可以使用 DirectShow **IFilterMapper2**接口来自动搜索满足特定条件的筛选器。 此应用程序可以使用建议的筛选器的列表， **IFilterMapper2**返回自动生成用于接收和呈现电视信号的筛选器的筛选器关系图。 若要快速查找符合指定条件的筛选器**IFilterMapper2**使用以前输入过到缓存中的筛选器，其插针，有关信息。 下面的段落中讨论所涉及到为此缓存*将固定数据缓存*。

Pin 数据缓存中包含的信息包括介质和筛选器可以公开每个 pin 的媒体类型的列表。 **IFilterMapper2**使用此缓存信息来确定可能的筛选器可以连接到已在关系图对筛选器的 pin。 在进行此决定消除了创建仅用于确定连接到该筛选器阻止，因为中等或媒体类型不匹配的筛选器的实例的系统开销。 如果筛选器的 pin 数据缓存不是最新的筛选器可能错误地消除作为筛选器关系图中的连接的候选项。

每当 BDA 微型驱动程序确定 DirectShow 使用其 pin 数据缓存不是最新，该微型驱动程序必须更新 pin 数据缓存，以便微型驱动程序的 BDA 组件的 BDA 筛选器实例的 pin 信息准确地公开在筛选器关系图。 BDA 微型驱动程序更新 DirectShow 的 pin 数据缓存在以下方案中所述：

-   BDA 微型驱动程序可能会或可能不需要更新 DirectShow 的 pin 数据缓存时微型驱动程序最初创建 BDA 筛选器实例，具体取决于该微型驱动程序如何显示，并且在用户模式下的 DirectShow 筛选器的 BDA 筛选器。 BDA 微型驱动程序的信息 (INF) 文件指定微型驱动程序使用来提供其 BDA 筛选器，如 DirectShow 筛选器的机制。

    BDA 微型驱动程序通常使用[内核流式处理 (KS) 代理模块](https://msdn.microsoft.com/library/windows/hardware/ff560877)(*Ksproxy.ax*) 以显示其 BDA 时，会筛选 DirectShow 筛选器。 KS 代理会自动更新 DirectShow 的 pin 数据缓存，以最初创建这些筛选器的实例时公开 BDA 筛选器的 pin 信息。 因此，不需要执行任何操作来更新 DirectShow 的 pin 数据缓存在最初创建筛选器的实例时使用 KS 代理的 BDA 微型驱动程序。 如果 BDA 筛选器公开为通过 KS 代理的用户模式时，缓存的信息会自动包括介质并立即后筛选器的筛选器实例存在的 pin 工厂的媒体类型创建调度例程返回。

    某些 BDA 微型驱动程序不使用 KS 代理提供其 BDA 将筛选器为 DirectShow 筛选器。 例如，BDA 接收方微型驱动程序实现 BDA 的筛选器以接收或进程模拟电视信号可以使用两种*KSTVTune.ax*或*KSXBar.ax*模块，以便显示作为这些 BDA 筛选器DirectShow 筛选器。 因为这些模块不使用标准 KS 代理接口方法更新 DirectShow 的 pin 数据缓存，对于这些类型的筛选器 BDA BDA 微型驱动程序必须更新 DirectShow 的 pin 数据缓存时这些微型驱动程序最初创建的筛选器实例。 为了确保在创建这些筛选器的实例时，更新 DirectShow 的 pin 数据缓存，BDA 微型驱动程序调用[ **BdaFilterFactoryUpdateCacheData** ](https://msdn.microsoft.com/library/windows/hardware/ff556455)后立即调用的函数[ **BdaInitFilter** ](https://msdn.microsoft.com/library/windows/hardware/ff556464)筛选器的实现内部函数的 create 调度例程。 在此调用中，微型驱动程序将更新的筛选器上的所有初始 pin 的 pin 信息传递。

-   Pin 可以 BDA 筛选器上动态创建后的筛选器创建调度例程完成。 如果 BDA 筛选器的最初创建的实例不会公开 BDA 筛选器的模板拓扑中列出的所有球瓶实例 ([**BDA\_筛选器\_模板**](https://msdn.microsoft.com/library/windows/hardware/ff556523))，然后 BDA 微型驱动程序必须调用**BdaFilterFactoryUpdateCacheData**强制有关筛选器的模板拓扑中列出的所有 pin 信息。

**请注意**  更新 DirectShow pin 数据缓存具有很大的开销，因为它涉及并修改注册表。 此外，更新 DirectShow 的 pin 数据缓存会影响所需的 DirectShow 自动生成筛选器关系图的时间量。 因此，BDA 微型驱动程序应调用**BdaFilterFactoryUpdateCacheData**所有可能的 pin 仅当确定使用 DirectShow 其 pin 数据缓存不是最新。

 

如果可能，应调用 BDA 微型驱动程序**BdaFilterFactoryUpdateCacheData**每当发生驱动程序、 固件或硬件更新。

 

 




