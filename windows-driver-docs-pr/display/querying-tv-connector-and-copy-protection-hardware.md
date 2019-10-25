---
title: 查询电视连接器和复制保护硬件
description: 查询电视连接器和复制保护硬件
ms.assetid: 7812a3ba-42f1-4872-bfe8-08933802f0c1
keywords:
- 电视连接器 WDK 视频微型端口
- 复制保护 WDK 视频微型端口，查询
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b475722e3bb701783d400cb1631334714fb4d8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829654"
---
# <a name="querying-tv-connector-and-copy-protection-hardware"></a>查询电视连接器和复制保护硬件


## <span id="ddk_querying_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_QUERYING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


具有电视连接器的适配器的视频微型端口驱动程序必须处理[**IOCTL\_视频\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)在其[*HWVIDSTARTIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)函数中处理\_VIDEOPARAMETERS 请求。 当 IOCTL 请求是 IOCTL\_视频\_句柄\_VIDEOPARAMETERS 时，视频的**InputBuffer**成员[ **\_请求\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)结构指向[**VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)结构。 该 VIDEOPARAMETERS 结构的**dwCommand**成员指定微型端口驱动程序是否必须提供有关电视连接器的信息（\_GET 的 VP\_命令）或将指定的设置应用于电视连接器（副总裁\_命令\_设置）。

当 VIDEOPARAMETERS 结构的**dwCommand**成员是\_获取的 VP\_命令时，微型端口驱动程序必须执行以下操作：

-   验证 VIDEOPARAMETERS 结构的**Guid**成员。

-   对于电视连接器支持的每项功能，请在 VIDEOPARAMETERS 结构的**dwFlags**成员中设置相应的标志。

-   对于**dwFlags**成员中设置的每个标志，将值分配给 VIDEOPARAMETERS 结构的相应成员，以指示与该标志关联的功能和当前设置。 有关对应于给定标志的结构成员的列表，请参阅[**VIDEOPARAMETERS**](https://docs.microsoft.com/windows/desktop/api/tvout/ns-tvout-_videoparameters)参考页。

VIDEOPARAMETERS 结构的**dwMode**成员指定电视输出是否经过优化，可用于视频播放或显示 Windows 桌面。 视频\_模式的值\_电视\_播放指定为视频播放优化电视输出（即禁用闪烁筛选器并启用 overscan）。 "视频\_模式"\_WIN\_图形的值指定为 Windows 图形优化电视输出（即启用最大闪烁筛选器并禁用 overscan）。

为了响应\_获取的 VP\_命令，微型端口驱动程序必须在**dwFlags**中设置副总裁\_标志\_电视\_模式标志，并且必须在**DWAVAILABLEMODES**中将 vp\_模式设置\_WIN\_图形位。 将\_模式\_电视\_播放位**设置为可选**。 此外，微型端口驱动程序必须在**dwFlags**中设置 VP\_标志\_最大\_无比例标志，并且必须为 VIDEOPARAMETERS 结构的相应成员赋值。

为了响应 VP\_命令\_获取，如果电视输出当前已禁用，微型端口驱动程序应将**dwMode**设置为0，将**DWTVSTANDARD**设置为 VP\_STANDARD\_WIN\_VGA，并设置**dwAvailableTVStandard**到 VP\_STANDARD\_WIN\_VGA。

示例1：适配器支持当前禁用的电视输出。 小型端口驱动程序必须执行以下操作，以响应\_获取的 VP\_命令：

-   在**dwFlags**中，将副总裁\_标志设置\_电视\_模式，将\_标志副总裁\_电视\_STANDARD，并将所有其他标志表示电视连接器支持的功能。

-   将**dwMode**设置为0。

-   在**dwAvailableModes**中，将 VP\_模式设置\_WIN\_图形。 如果硬件支持副总裁\_模式\_电视\_播放，则同时设置该位。

-   将**dwTVStandard**设置为副总裁\_TV\_STANDARD\_WIN\_VGA。

-   在**dwAvailableTVStandard**中，设置代表电视连接器支持的电视标准的所有位。

-   对于在**dwFlags**中设置的所有标志（除了\_标志的 VP 标志\_电视\_模式和副总裁\_\_标志），请将值分配给 VIDEOPARAMETERS 的相应成员。构造.

示例2：若要启用电视输出，调用方（而非微型端口驱动程序）应执行以下操作：

-   在**dwFlags**中，将副总裁\_标志\_电视\_模式和副总裁\_标志\_\_STANDARD。 清除所有其他标志。

-   将**dwMode**设置为 VP\_模式\_WIN\_图形或副总裁\_模式\_TV\_播放。 不要设置这两个位。

-   将**dwTvStandard**设置为所需标准（例如副总裁\_TV\_STANDARD\_NTSC\_M）。 不要在**dwTvStandard**中设置任何其他位。

示例3：若要禁用电视输出，调用方（而非微型端口驱动程序）应执行以下操作：

-   在**dwFlags**中，将副总裁\_标志\_电视\_模式和副总裁\_标志\_\_STANDARD。 清除所有其他标志。

-   将**dwMode**设置为0。

-   在**dwTvStandard**中，将副总裁\_TV\_STANDARD\_WIN\_VGA。 清除**dwTvStandard**中的所有其他位。

 

 





