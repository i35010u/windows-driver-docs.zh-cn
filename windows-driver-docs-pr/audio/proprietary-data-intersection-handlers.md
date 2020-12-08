---
title: 专有数据交集处理程序
description: 专有数据交集处理程序
keywords:
- 数据交集处理程序 WDK 音频，专用
- 专用数据交集处理程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e04cde38fde7326764f2fac59b425a51fa0d0d6a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800785"
---
# <a name="proprietary-data-intersection-handlers"></a>专有数据交集处理程序


## <span id="proprietary_data_intersection_handlers"></span><span id="PROPRIETARY_DATA_INTERSECTION_HANDLERS"></span>


可以通过编写适配器的专有处理程序来克服默认数据交集处理程序的限制。 专用处理程序在微型端口驱动程序对象上实现为 [**IMiniport：:D atarangeintersection**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection) 方法。 有关 **DataRangeIntersection** 方法的示例，请参阅 Microsoft Windows 驱动程序工具包 (WDK) 中的示例适配器驱动程序。

专有的数据交集处理程序可以对无法在 [**KSDATARANGE \_ 音频**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio) 结构中充分指定的非标准硬件功能进行补偿。 例如，WDK 中的 AC97 示例适配器驱动程序管理可在播放期间支持两个或更多音频通道但不支持 mono 的硬件。 该示例的 [**DataRangeIntersection**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection) 方法确定是否将其他筛选器的源 pin 的数据范围限制为单声道 (即 **MaximumChannels** &lt; 2) 。 如果是这样，则通过返回 "无匹配" 状态来调用失败 \_ \_ 。

专有的数据交集处理程序可以选择处理其某些插针上的数据交集，并允许端口驱动程序的默认数据交集处理程序处理其他插针上的数据交集。

本部分的其余部分介绍了实现专用数据交集处理程序的准则。

 

