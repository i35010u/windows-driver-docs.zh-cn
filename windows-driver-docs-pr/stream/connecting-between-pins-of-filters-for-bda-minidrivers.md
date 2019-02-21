---
title: Pin BDA 微型驱动程序的筛选器之间的连接
description: Pin BDA 微型驱动程序的筛选器之间的连接
ms.assetid: 549031f3-1501-43c0-b172-bc88613d7e61
keywords:
- 广播驱动程序体系结构 WDK AVStream，pin 数据范围
- BDA WDK AVStream，pin 数据范围
- 数据范围 WDK AVStream
- 范围 WDK AVStream
- 将数据区域固定 WDK
- 将固定连接 WDK BDA
- 连接插针 WDK BDA
- 连接 WDK BDA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e35c6ab3cd37933b211526363154c9dcbd544c1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543559"
---
# <a name="connecting-between-pins-of-filters-for-bda-minidrivers"></a>Pin BDA 微型驱动程序的筛选器之间的连接





若要使 BDA 筛选器的插针连接到对方，BDA 微型驱动程序的这些筛选器必须提供的列表数据区域球瓶中所述[AVStream 中的数据范围交集](data-range-intersections-in-avstream.md)。 换而言之，筛选器的插针指定它们支持以启用 pin 的其他筛选器也支持这些数据区域的流连接的数据范围。

例如，若要让 BDA pin 调谐器和捕获筛选器，输出插针连接的调谐器筛选器和捕获筛选器输入插针必须具有以下设置的数据格式[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)球瓶的结构：

-   **MajorFormat**设置为静态\_KSDATAFORMAT\_类型\_流

-   **子格式**设置为静态\_KSDATAFORMAT\_类型\_MPEG2\_传输

-   **说明符**设置为静态\_KSDATAFORMAT\_说明符\_BDA\_传输

若要让 BDA pin 捕获和 demultiplex 筛选器，输出插针连接的捕获筛选器和 demultiplex 筛选器输入插针必须具有以下设置的数据格式[ **KSDATARANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff561658)球瓶的结构：

-   **MajorFormat**设置为静态\_KSDATAFORMAT\_类型\_流

-   **子格式**设置为静态\_KSDATAFORMAT\_子类型\_BDA\_MPEG2\_传输

-   **说明符**设置为静态\_KSDATAFORMAT\_说明符\_NONE

**请注意**  只能对静态设置 demultiplex 筛选器的输入插针\_KSDATAFORMAT\_子类型\_BDA\_MPEG2\_传输 subformat 如果 AVStream微型驱动程序的筛选器是 BDA 兼容。
如果的媒体类型的输入的插针设置为静态\_KSDATAFORMAT\_子类型\_BDA\_MPEG2\_传输和筛选器将不符合 BDA 规则、 广播的信号可能不会正确呈现。

 

 

 




