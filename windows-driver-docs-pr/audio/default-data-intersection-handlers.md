---
title: 默认数据交集处理程序
description: 默认数据交集处理程序
keywords:
- 数据交集处理程序 WDK 音频，默认
- 默认数据交集处理程序
- 最小数据交集处理程序 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a8fb8ea86398ffb9dfff845c7f631210eb410a4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784877"
---
# <a name="default-data-intersection-handlers"></a>默认数据交集处理程序


## <span id="default_data_intersection_handlers"></span><span id="DEFAULT_DATA_INTERSECTION_HANDLERS"></span>


适配器的专用数据交集处理程序 (微型端口驱动程序对象的 [**IMiniport：:D atarangeintersection**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiport-datarangeintersection) 方法) 可以通过返回状态 " \_ 未实现" 状态代码来拒绝执行数据交集检查 \_ 。 在这种情况下，端口驱动程序的默认数据交集处理程序会代表适配器执行检查。

可以将适配器驱动程序的最小数据交集处理程序实现为 **DataRangeIntersection** 方法，该方法通过返回未实现的状态来拒绝所有数据交集请求 \_ \_ 。

端口驱动程序的默认处理程序的当前实现仅限于它可以处理的数据范围类型：

-   仅 PCM 数据格式

-   仅 mono 和立体声音频流

支持非 PCM 或多通道格式的适配器驱动程序应实现专用的数据交集处理程序，而不是依赖于端口驱动程序来处理这些格式的数据交集。

此外，默认处理程序仅支持可由 [**KSDATAFORMAT \_ DSOUND**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_dsound) 或 [**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex) 结构指定的音频格式。 它不支持包含 [**WAVEFORMATEXTENSIBLE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-waveformatextensible) 结构的任何格式，例如，需要为具有两个以上通道的格式指定通道掩码。

从两个数据区域的交集中选择通用格式时，端口驱动程序的默认处理程序始终在每个参数的交集区域中选择最大值：

-   如果交集跨越多个有效的采样频率 (11、22和 44 kHz，如) ，则默认处理程序将选取最高的频率。

-   如果交集跨多个有效位数 (8、16和32位，例如) ，则默认处理程序选取最大值。

-   如果交集同时跨越 mono 和立体声格式，则默认处理程序将选取立体声。

如果默认处理程序选择了不满意的格式，则适配器驱动程序可以选择通过 **newstream.ischecked** 调用拒绝该格式 (例如，在 SysAudio 尝试使用格式创建接收器 pin 时，请参阅 [**IMiniportWavePci：： newstream.ischecked**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iminiportwavepci-newstream)) 。 如果调用失败，SysAudio 将不会继续查找数据交集。 相反，它将尝试通过以下方式来创建连接：遍历系统筛选器支持的 PCM 格式列表（如 KMixer），直到找到适配器接收器 pin 还可以支持的这些类型。 此列表首先按更高质量格式排序。 与之前一样，适配器通过使这些格式的 **newstream.ischecked** 调用失败，拒绝列表中不满意的格式。

 

