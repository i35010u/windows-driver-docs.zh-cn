---
title: 缓存 DirectShow 的引脚信息
description: 缓存 DirectShow 的引脚信息
ms.assetid: 1e6a973b-32d2-4ac2-9cd6-f4d3c329cecf
keywords:
- 固定数据缓存 WDK BDA
- 缓存 WDK AVStream
- DirectShow 固定数据缓存 WDK AVStream
- 更新 pin 数据缓存 WDK AVStream
- 广播驱动程序体系结构 WDK AVStream，固定数据缓存
- BDA WDK AVStream，固定数据缓存
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80cd564d282a9c437805d94d6d0726d3364173c1
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186177"
---
# <a name="caching-pin-information-for-directshow"></a>缓存 DirectShow 的引脚信息





应用程序可以使用 DirectShow **IFilterMapper2** 接口自动搜索符合特定条件的筛选器。 此应用程序可使用 **IFilterMapper2** 返回的建议筛选器列表，自动生成筛选器图形，其中包含接收和呈现电视信号的筛选器。 为了快速查找满足指定条件的筛选器， **IFilterMapper2** 使用了有关筛选器及其之前输入缓存的 pin 的信息。 以下段落中的讨论将此缓存称为 *pin 数据缓存*。

Pin 数据缓存中包含的信息包括媒体的列表和筛选器可以公开的每个 pin 的媒体类型。 **IFilterMapper2** 使用此缓存信息来确定可能的筛选器是否可以连接到已在图形中的筛选器上的 pin。 做出此决定消除了创建筛选器实例的开销，只是为了确定由于介质或介质类型不匹配而阻止连接到筛选器。 如果筛选器的 pin 数据缓存不是最新的，则可能会错误地消除筛选器，作为筛选器关系图中的连接的候选项。

只要 BDA 微型驱动程序确定 DirectShow 使用的 pin 数据缓存不是最新的，则微型驱动程序必须更新 pin 数据缓存，以便在筛选器图中准确地公开微型驱动程序的 BDA 组件的 BDA 筛选器实例的 pin 信息。 BDA 微型驱动程序会更新 DirectShow 的 pin 数据缓存，如以下方案所述：

-   当微型驱动程序最初根据微型驱动程序将 BDA 筛选器以用户模式显示为 DirectShow 筛选器时，微型驱动程序可能需要也可能不需要更新 DirectShow 的 pin 数据缓存。 BDA 微型驱动程序的信息 (INF) 文件指定了微型驱动程序用来将它的 BDA 筛选器呈现为 DirectShow 筛选器的机制。

    BDA 微型驱动程序通常使用 [内核流式处理 (KS) proxy 模块](/windows-hardware/drivers/ddi/_stream/index) (*Ksproxy.ax*) 将其 BDA 筛选器显示为 DirectShow 筛选器。 当最初创建了这些筛选器的实例时，KS 代理会自动更新 DirectShow 的 pin 数据缓存，以便公开 BDA 筛选器的 pin 信息。 因此，在最初创建筛选器的实例时，不需要使用 KS 代理来执行任何操作来更新 DirectShow 的 pin 数据缓存。 如果通过 KS proxy 向用户模式公开 BDA 筛选器，缓存的信息将自动包括在筛选器的创建调度例程返回后，位于筛选器实例上的 pin 工厂的媒体和媒体类型。

    某些 BDA 微型驱动程序不会使用 KS 代理以 DirectShow 筛选器形式显示其 BDA 筛选器。 例如，用于实现 BDA 筛选器以接收或处理模拟电视信号的 BDA 接收方微型驱动程序使用 *KSTVTune.ax* 或 *KSXBar.ax* 模块将这些 BDA 筛选器呈现为 DirectShow 筛选器。 由于这些模块不使用标准 KS 代理接口方法来更新 DirectShow 的 pin 数据缓存，因此这些类型的 BDA 筛选器的 BDA 微型驱动程序必须在微型驱动程序最初创建筛选器实例时更新 DirectShow 的 pin 数据缓存。 为了确保在创建这些筛选器的实例时，将更新 DirectShow 的 pin 数据缓存，BDA 微型驱动程序会在调用[**BdaInitFilter**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdainitfilter)函数后立即调用[**BdaFilterFactoryUpdateCacheData**](/windows-hardware/drivers/ddi/bdasup/nf-bdasup-bdafilterfactoryupdatecachedata)函数，这是在筛选器的 create 调度例程的实现中。 在此调用中，微型驱动程序将传递 pin 信息以更新筛选器上的所有初始 pin。

-   在筛选器的创建调度例程完成后，可在 BDA 筛选器上动态创建 pin。 如果 "bda 筛选器" 的初始创建实例不公开 "bda 筛选器" 的模板拓扑中列出的所有 pin 的实例 ([**bda \_ 筛选器 \_ 模板**](/windows-hardware/drivers/ddi/bdasup/ns-bdasup-_bda_filter_template)) ，则 BDA 微型驱动程序必须调用 **BdaFilterFactoryUpdateCacheData** 来强制执行有关筛选器模板拓扑中列出的所有 pin 的信息。

**注意**   更新 DirectShow 的 pin 数据缓存会产生很大的开销，因为它涉及并修改注册表。 此外，更新 DirectShow 的 pin 数据缓存会影响 DirectShow 自动生成筛选器关系图所需的时间量。 因此，仅当 BDA 微型驱动程序确定 DirectShow 使用的 pin 数据缓存不是最新时，才应为所有可能的 pin 调用 **BdaFilterFactoryUpdateCacheData** 。

 

如果可能，在出现驱动程序、固件或硬件更新时，BDA 微型驱动程序应调用 **BdaFilterFactoryUpdateCacheData** 。

 

