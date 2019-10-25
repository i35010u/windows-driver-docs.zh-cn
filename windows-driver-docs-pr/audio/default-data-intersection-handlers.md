---
title: 默认数据交集处理程序
description: 默认数据交集处理程序
ms.assetid: 5c70a6e4-702f-4fd0-bb3e-2cde2955b2ad
keywords:
- 数据交集处理程序 WDK 音频，默认
- 默认数据交集处理程序
- 最小数据交集处理程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe9d764e06dacfe4c2afd01acf701a2919acfc16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833560"
---
# <a name="default-data-intersection-handlers"></a>默认数据交集处理程序


## <span id="default_data_intersection_handlers"></span><span id="DEFAULT_DATA_INTERSECTION_HANDLERS"></span>


适配器的专用数据交集处理程序（微型端口驱动程序对象的[**IMiniport：:D atarangeintersection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection)方法）可以拒绝通过返回状态\_未\_实现的状态来执行数据交集检查编写. 在这种情况下，端口驱动程序的默认数据交集处理程序会代表适配器执行检查。

可以将适配器驱动程序的最小数据交集处理程序实现为**DataRangeIntersection**方法，该方法通过返回状态\_未\_实现的状态来拒绝所有数据交集请求。

端口驱动程序的默认处理程序的当前实现仅限于它可以处理的数据范围类型：

-   仅 PCM 数据格式

-   仅 mono 和立体声音频流

支持非 PCM 或多通道格式的适配器驱动程序应实现专用的数据交集处理程序，而不是依赖于端口驱动程序来处理这些格式的数据交集。

此外，默认处理程序仅支持可由[**KSDATAFORMAT\_DSOUND**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound)或[**KSDATAFORMAT\_WAVEFORMATEX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex)结构指定的音频格式。 它不支持包含[**WAVEFORMATEXTENSIBLE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible)结构的任何格式，例如，需要为具有两个以上通道的格式指定通道掩码。

从两个数据区域的交集中选择通用格式时，端口驱动程序的默认处理程序始终在每个参数的交集区域中选择最大值：

-   如果交集跨越多个有效的采样频率（例如11、22和 44 kHz），则默认处理程序将选取最高的频率。

-   如果交集跨越多个有效的每样本位数（例如8、16和32位），则默认处理程序将选取最大的值。

-   如果交集同时跨越 mono 和立体声格式，则默认处理程序将选取立体声。

如果默认处理程序选择的格式不满意，则在 SysAudio 尝试创建接收器 pin 时，适配器驱动程序可以选择**拒绝该格式**（例如，请参阅[**IMiniportWavePci：： newstream.ischecked**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)）格式为。 如果调用失败，SysAudio 将不会继续查找数据交集。 相反，它将尝试通过以下方式来创建连接：遍历系统筛选器支持的 PCM 格式列表（如 KMixer），直到找到适配器接收器 pin 还可以支持的这些类型。 此列表首先按更高质量格式排序。 与之前一样，适配器通过使这些格式的**newstream.ischecked**调用失败，拒绝列表中不满意的格式。

 

 




