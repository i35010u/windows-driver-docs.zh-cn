---
title: 默认数据交集处理程序
description: 默认数据交集处理程序
ms.assetid: 5c70a6e4-702f-4fd0-bb3e-2cde2955b2ad
keywords:
- 数据交集处理程序 WDK 音频，默认值
- 默认数据交集的处理程序
- 最小数据交集处理程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aee3aeb9c615367bffd158854158373c757320e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333918"
---
# <a name="default-data-intersection-handlers"></a>默认数据交集处理程序


## <span id="default_data_intersection_handlers"></span><span id="DEFAULT_DATA_INTERSECTION_HANDLERS"></span>


适配器的专有数据交集处理程序 (微型端口驱动程序对象的[ **IMiniport::DataRangeIntersection** ](https://msdn.microsoft.com/library/windows/hardware/ff536764)方法) 可以拒绝通过返回执行数据交集检查状态\_不\_实现状态代码。 在这种情况下，端口驱动程序的默认数据交集处理程序执行以适配器名义检查。

您可以实现的最小数据交集处理程序适配器驱动程序，因为**DataRangeIntersection**拒绝数据相交的所有请求通过返回状态的方法\_不\_实现。

端口驱动程序的默认处理程序的当前实现中它可以处理的数据范围的类型限制：

-   只有 PCM 数据格式

-   仅 mono 和立体声音频流

支持非 PCM 或多通道格式的适配器驱动程序应实现而不是依靠端口驱动程序处理这些格式的数据交集的专有数据交集处理程序。

此外，默认处理程序仅支持音频格式，可以通过指定[ **KSDATAFORMAT\_DSOUND** ](https://msdn.microsoft.com/library/windows/hardware/ff537094)或[ **KSDATAFORMAT\_WAVEFORMATEX** ](https://msdn.microsoft.com/library/windows/hardware/ff537095)结构。 不支持任何格式包含[ **WAVEFORMATEXTENSIBLE** ](https://msdn.microsoft.com/library/windows/hardware/ff538802)结构，它需要使用，例如，指定一种格式通道掩码与两个以上声道。

在选择一种通用格式时从两个数据区域之间的交集，端口驱动程序的默认处理程序始终在每个参数的交集的区域中选择的最大值：

-   如果交集跨越多个有效的采样频率 （11、 22 和 44 kHz，例如） 的默认处理程序选取最高的频率。

-   如果交集跨多个有效位每个示例值 （8、 16 和 32 位，例如），默认处理程序会选取的最大值。

-   如果交集跨 mono 和立体声格式，默认处理程序会选取立体声。

如果默认处理程序选择不令人满意的格式，适配器驱动程序可以选择拒绝被失败的格式**NewStream**调用 (有关示例，请参阅[ **IMiniportWavePci::NewStream** ](https://msdn.microsoft.com/library/windows/hardware/ff536735)) SysAudio 尝试使用格式创建接收器 pin。 如果调用失败，SysAudio 将继续查找数据交集。 相反，它将尝试通过遍历直到它找到一个适配器的接收器 pin 可以支持还受系统筛选器，例如 KMixer PCM 格式的列表中创建的连接。 列表是第一次排序具有更高质量格式。 如前面一样，则适配器将拒绝被失败的列表中不令人满意的格式**NewStream**调用为这些格式。

 

 




