---
title: 在 BDA 微型驱动程序筛选器的引脚之间进行连接
description: 在 BDA 微型驱动程序筛选器的引脚之间进行连接
ms.assetid: 549031f3-1501-43c0-b172-bc88613d7e61
keywords:
- 广播驱动程序体系结构 WDK AVStream，固定数据范围
- BDA WDK AVStream，固定数据范围
- 数据范围 WDK AVStream
- 范围 WDK AVStream
- 固定数据范围 WDK
- 固定连接 WDK BDA
- 连接引脚 WDK BDA
- 连接 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95b379029c1b8e6c053c9905295ede4c0a9ed6ef
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184169"
---
# <a name="connecting-between-pins-of-filters-for-bda-minidrivers"></a>在 BDA 微型驱动程序筛选器的引脚之间进行连接





为了使 BDA 筛选器的 pin 相互连接，这些筛选器的 BDA 微型驱动程序必须提供 pin 的数据范围列表，如 [AVStream 中的数据范围交集](data-range-intersections-in-avstream.md)中所述。 换句话说，筛选器的 pin 将指定它们支持的数据范围，以启用到支持这些数据范围的其他筛选器的 pin 的流连接。

例如，若要允许 pin 调谐器的 pin 和捕获筛选器连接，调谐器筛选器的输出插针和捕获筛选器的输入插针必须在 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构中为 pin 设置以下数据格式：

-   **MajorFormat** 设置为 STATIC \_ KSDATAFORMAT \_ 类型 \_ 流

-   **SubFormat** 设置为 STATIC \_ KSDATAFORMAT \_ 类型 \_ MPEG2 \_ TRANSPORT

-   **Specifier**设置为 STATIC \_ KSDATAFORMAT \_ 说明符 \_ BDA \_ 传输的说明符

若要允许引脚捕获和 demultiplex 筛选器连接，必须在 pin 的 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构中设置捕获筛选器和 demultiplex 筛选器的输入插针的以下数据格式：

-   **MajorFormat** 设置为 STATIC \_ KSDATAFORMAT \_ 类型 \_ 流

-   **SubFormat** 设置为 STATIC \_ KSDATAFORMAT \_ 子类型 \_ BDA \_ MPEG2 \_ TRANSPORT

-   **说明符** 设置为 STATIC \_ KSDATAFORMAT \_ 说明符 \_ NONE

**注意**   仅可将 demultiplex 筛选器的输入插针设置为静态 \_ KSDATAFORMAT \_ 子类型 \_ BDA \_ MPEG2 \_ 传输 subformat，前提是筛选器的 AVStream 微型驱动程序符合 BDA。
如果输入插针的媒体类型设置为 STATIC \_ KSDATAFORMAT \_ 子类型 \_ BDA \_ MPEG2 传输， \_ 并且筛选器不符合 BDA 规则，则广播信号可能无法正确呈现。

 

 

