---
title: KS 微型驱动程序体系结构
description: KS 微型驱动程序体系结构
keywords:
- 内核流 WDK，体系结构
- KS WDK，体系结构
- 筛选器关系图 WDK 内核流式处理
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: 51e482ffa3c4dbbe796315004e3604cf3a109afc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838541"
---
# <a name="ks-minidriver-architecture"></a>KS 微型驱动程序体系结构

内核流式处理服务支持流式处理数据的内核模式处理。 在此模型中，流数据流经分组到块（称为筛选器）的一系列节点。 每个筛选器封装了对数据执行的某个处理任务。 [KS 筛选器](ks-filters.md)作为内核模式 [**驱动程序 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_driver_object)实现。

在用户模式下，KS 筛选器将通过代理作为 DirectShow 筛选器出现。 因此，图形生成器和用户模式应用程序可以与 KS 筛选器进行交互。 在活动图中，内核模式组件仍直接通信，消除了用户模式和内核模式间的资源消耗转换。

数据流入和流出连接点（称为 [pin](ks-pins.md)）的筛选器。 Pin 实例呈现或捕获数据流，如数字音频。

筛选器图是一组已连接的筛选器。 筛选器关系图将链接多个要在流上执行的处理任务。 您可以使用 Microsoft Windows 驱动程序工具包 (WDK) 中的 GraphEdit 工具测试各种 [筛选器图形配置](filter-graph-examples.md) 。 有关的详细信息，请参阅 [筛选器图形编辑器工具](/windows/win32/directshow/simulating-graph-building-with-graphedit) 网站。

支持 [板上时钟](ks-clocks.md) 的驱动程序将时钟作为文件对象公开。 微型驱动程序可以 [查询时钟时间](./kspropsetid-clock.md)，或在时钟到达特定时间时 [**通知请求**](./kseventsetid-clock.md) 。

支持自定义内存管理接口的微型驱动程序将此接口作为称为 [分配](ks-allocators.md)器的文件对象公开。 例如，处理机载内存的设备管理器可能会暴露此类接口。 然后，微型驱动程序可以使用相关的文件对象来分配和释放内存。

本部分包含有关以下主题的其他信息：

[KS 筛选器](ks-filters.md)

[KS 引脚](ks-pins.md)

[KS 数据格式和数据范围](ks-data-formats-and-data-ranges.md)

[KS 媒体](ks-mediums.md)

[KS 接口](ks-interfaces.md)

[质量管理](quality-management.md)
