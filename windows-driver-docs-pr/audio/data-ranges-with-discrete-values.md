---
title: 具有离散值的数据范围
description: 具有离散值的数据范围
ms.assetid: 330edd60-0469-4351-bfb1-29b29e133c1a
keywords:
- 数据交集处理程序 WDK 音频的离散值的数据范围
- 离散值的数据范围 WDK 音频
- 数据范围 WDK 音频的离散值
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2c207abc3f09aeeef005d546c46f96557bfc18b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359086"
---
# <a name="data-ranges-with-discrete-values"></a>具有离散值的数据范围


## <span id="data_ranges_with_discrete_values"></span><span id="DATA_RANGES_WITH_DISCRETE_VALUES"></span>


如果音频设备支持的 11、 22 和 44 kHz 示例频率为例，你可以为在单个范围为 11 到 44 kHz 指定所有三个频率[ **KSDATARANGE\_音频**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-ksdatarange_audio)结构. 此方法具有简洁的好处。 潜在的缺点是错误的数据交叉处理程序可以选择在范围内的无效的参数值 (例如，27 kHz)。 在这种情况下，适配器驱动程序已失败但没有选项**NewStream**调用 (有关示例，请参阅[ **IMiniportWavePci::NewStream**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavepci-newstream)) 可用于创建 pin格式无效。

另一种方法是为每个参数提供的数据区域中的每个数据区域指定一个离散值而不是一系列值列表。 例如，而不是提供单个数据范围，以指定一系列示例频率从 11 到 44 kHz，数据范围数组可以包含三个单独元素 11、 22 和 44 kHz。 在每个元素，最大和最小示例频率设置为相同的值 （11、 22 或 44 kHz）。 此方法的好处是，它解决了有关支持的精确值不明确性。 此外，如果一个离散值优于另一个，包含此值的数据范围可以移动到数组，它是之前包含其他值的数据范围中的位置。 次要的离散值的缺点是它们可以提高数据范围数组的大小。

 

 




