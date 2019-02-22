---
title: KS 微型驱动程序体系结构
description: KS 微型驱动程序体系结构
ms.assetid: a9c17040-72a8-4290-831b-7fb46b00f532
keywords:
- 流式处理 WDK，体系结构的内核
- KS WDK，体系结构
- 筛选器关系图 WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87a7e23238e8591b73542fba72108da94d028667
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520108"
---
# <a name="ks-minidriver-architecture"></a>KS 微型驱动程序体系结构





流式处理的流数据服务支持内核模式下处理的内核。 在此模型中，流式传输数据流通过一系列分组到块的节点称为筛选器。 每个筛选器封装要对数据执行一些处理任务。 一个[KS 筛选器](ks-filters.md)作为内核模式下实现[**驱动程序\_对象**](https://msdn.microsoft.com/library/windows/hardware/ff544174)。

通过代理服务器，KS 筛选器显示为在用户模式下的 DirectShow 筛选器。 在这种情况下，图形生成器和用户模式应用程序可以与 KS 筛选器进行交互。 在活动图形中，内核模式组件仍直接进行通信，消除消耗资源的用户模式和内核模式之间的转换。

数据流入流出在连接点的筛选器称为[pin](ks-pins.md)。 Pin 实例呈现或捕获数据的流，如数字音频。

筛选器关系图是一组已连接的筛选器。 筛选器图形链接在流上执行多个处理任务。 你可以测试各种[筛选器图形配置](filter-graph-examples.md)使用 GraphEdit 工具在 Microsoft Windows 驱动程序工具包 (WDK)。 (有关 GraphEdit 详细信息，请参阅[筛选器关系图编辑器工具](https://go.microsoft.com/fwlink/p/?linkid=9230)网站。)

支持的驱动程序[板载时钟](ks-clocks.md)公开作为文件对象的时钟。 微型驱动程序可以[查询的时钟时间](https://msdn.microsoft.com/library/windows/hardware/ff566564)，或者[**请求通知**](https://msdn.microsoft.com/library/windows/hardware/ff561764)时钟在到达特定时间。

支持自定义内存管理界面的微型驱动程序作为名为的文件对象公开此接口[分配器](ks-allocators.md)。 例如，设备管理器处理载入内存可能会使此类接口。 然后，微型驱动程序可以使用相关的文件对象来分配和释放内存。

本部分包含有关以下主题的其他信息：

[KS 筛选器](ks-filters.md)

[KS Pin](ks-pins.md)

[KS 数据格式和数据区域](ks-data-formats-and-data-ranges.md)

[KS 媒体](ks-mediums.md)

[KS 接口](ks-interfaces.md)

[质量管理](quality-management.md)

 

 




