---
title: 专有数据交集处理程序
description: 专有数据交集处理程序
ms.assetid: 8ed497d3-2344-4979-9859-e66a4713e6c5
keywords:
- 数据交集处理程序 WDK 音频专有
- 专有数据交集处理程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c2b2ce7a592c5a848c37a53fe7f079023442049
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67362524"
---
# <a name="proprietary-data-intersection-handlers"></a>专有数据交集处理程序


## <span id="proprietary_data_intersection_handlers"></span><span id="PROPRIETARY_DATA_INTERSECTION_HANDLERS"></span>


可以通过为您的适配器编写的专有的处理程序来克服的默认数据交集处理程序的限制。 专有的处理程序作为[ **IMiniport::DataRangeIntersection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-datarangeintersection)微型端口驱动程序对象上的方法。 请参阅示例适配器驱动程序在 Microsoft Windows 驱动程序工具包 (WDK) 有关的示例**DataRangeIntersection**方法。

专有数据交集处理程序可以不能充分中指定的非标准的硬件功能来补救[ **KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)结构。 例如，在 WDK 中的 AC97 示例适配器驱动程序管理硬件，可以在播放期间，支持两个或多个音频通道，但不能支持 mono。 该示例的[ **DataRangeIntersection** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiport-datarangeintersection)方法确定是否其他筛选器的源 pin 的数据范围仅限于 mono (即**MaximumChannels** &lt; 2)。 如果因此，它无法进行调用的返回状态\_否\_匹配项。

专有数据交集处理程序可以处理某些其插针上的数据交集，并允许端口驱动程序的默认数据交集处理程序的选择来处理数据在其他球瓶的交集。

本部分的其余部分提供了实现专有数据交集处理程序的准则。

 

 




