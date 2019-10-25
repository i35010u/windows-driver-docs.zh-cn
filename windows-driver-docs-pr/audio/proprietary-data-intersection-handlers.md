---
title: 专有数据交集处理程序
description: 专有数据交集处理程序
ms.assetid: 8ed497d3-2344-4979-9859-e66a4713e6c5
keywords:
- 数据交集处理程序 WDK 音频，专用
- 专用数据交集处理程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e4ad0a7ee592021c06ce44480b8c4a95bf3b125
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72830225"
---
# <a name="proprietary-data-intersection-handlers"></a>专有数据交集处理程序


## <span id="proprietary_data_intersection_handlers"></span><span id="PROPRIETARY_DATA_INTERSECTION_HANDLERS"></span>


可以通过编写适配器的专有处理程序来克服默认数据交集处理程序的限制。 专用处理程序在微型端口驱动程序对象上实现为[**IMiniport：:D atarangeintersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)方法。 有关**DataRangeIntersection**方法的示例，请参阅 Microsoft Windows 驱动程序工具包（WDK）中的示例适配器驱动程序。

专有的数据交集处理程序可以对不能在[**KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdatarange_audio)结构中充分指定的非标准硬件功能进行补偿。 例如，WDK 中的 AC97 示例适配器驱动程序管理可在播放期间支持两个或更多音频通道但不支持 mono 的硬件。 该示例的[**DataRangeIntersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)方法确定是否将其他筛选器的源 pin 的数据范围限制为 mono （即， **MaximumChannels** &lt; 2）。 如果是这样，则无法通过返回状态\_\_不匹配来进行调用。

专有的数据交集处理程序可以选择处理其某些插针上的数据交集，并允许端口驱动程序的默认数据交集处理程序处理其他插针上的数据交集。

本部分的其余部分介绍了实现专用数据交集处理程序的准则。

 

 




