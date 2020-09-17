---
title: 查询电视连接器和复制保护硬件
description: 查询电视连接器和复制保护硬件
ms.assetid: 7812a3ba-42f1-4872-bfe8-08933802f0c1
keywords:
- 电视连接器 WDK 视频微型端口
- 复制保护 WDK 视频微型端口，查询
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbc7a7d8973d5500a2c2072b3254ab4ea3f24689
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715812"
---
# <a name="querying-tv-connector-and-copy-protection-hardware"></a>查询电视连接器和复制保护硬件


## <span id="ddk_querying_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_QUERYING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


具有电视连接器的适配器的视频微型端口驱动程序必须处理其[*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)函数中的[**IOCTL \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)请求。 当 IOCTL 请求为 IOCTL \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS 时，[**视频 \_ 请求 \_ 包**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)结构的**InputBuffer**成员指向[**VIDEOPARAMETERS**](/windows/win32/api/tvout/ns-tvout-_videoparameters)结构。 该 VIDEOPARAMETERS 结构的 **dwCommand** 成员指定微型端口驱动程序是否必须提供有关 tv 连接器 (vp \_ 命令 GET) 的信息， \_ 或者将指定的设置应用于电视连接器 (vp \_ 命令 \_ 集) 。

当 VIDEOPARAMETERS 结构的 **dwCommand** 成员为 VP \_ 命令 GET 时 \_ ，微型端口驱动程序必须执行以下操作：

-   验证 VIDEOPARAMETERS 结构的 **Guid** 成员。

-   对于电视连接器支持的每项功能，请在 VIDEOPARAMETERS 结构的 **dwFlags** 成员中设置相应的标志。

-   对于 **dwFlags** 成员中设置的每个标志，将值分配给 VIDEOPARAMETERS 结构的相应成员，以指示与该标志关联的功能和当前设置。 有关对应于给定标志的结构成员的列表，请参阅 [**VIDEOPARAMETERS**](/windows/win32/api/tvout/ns-tvout-_videoparameters) 参考页。

VIDEOPARAMETERS 结构的 **dwMode** 成员指定电视输出是否经过优化，可用于视频播放或显示 Windows 桌面。 视频 \_ 模式 \_ 电视节目的值 \_ 指定将电视输出优化为视频播放 (也就是说，禁用闪烁筛选器并) 启用 overscan。 "视频 \_ 模式 \_ WIN \_ 图形" 的值指定为 WINDOWS 图形优化电视输出 (即启用最大闪烁筛选器并) 禁用 overscan。

为响应 VP \_ 命令 \_ GET，微型端口驱动程序必须 \_ \_ 在 dwFlags 中设置 vp 标志电视 \_ 模式**dwFlags**标志，并且必须 \_ 在 dwAvailableModes 中设置副总裁模式 \_ WIN \_ 图形位。 **dwAvailableModes** \_在 dwAvailableModes 中设置副总裁模式 \_ 电视 \_ 播放位是可选的。 **dwAvailableModes** 此外，微型端口驱动程序必须 \_ \_ 在 dwFlags 中设置 VP 标志最大无 \_ 比例标志，并且必须为 VIDEOPARAMETERS 结构的相应成员分配值。 **dwFlags**

为了响应 VP \_ 命令 \_ GET，如果电视输出当前被禁用，微型端口驱动程序应将 **dwMode** 设置为0，将 **dwTVStandard** 设置为 " \_ 标准 \_ win \_ vga"，将 " **dwAvailableTVStandard** " 设置为 "副总裁" \_ 标准 \_ win \_ vga。

示例1：适配器支持当前禁用的电视输出。 小型端口驱动程序必须执行以下操作，以响应 VP \_ 命令 \_ GET：

-   在 **dwFlags**中，设置副总裁 \_ 标志 \_ 电视 \_ 模式，副总裁 \_ 标志 \_ 电视 \_ 标准，以及代表 tv 连接器支持的功能的所有其他标志。

-   将 **dwMode** 设置为0。

-   在 **dwAvailableModes**中，设置副总裁 \_ 模式 \_ WIN \_ 图形。 如果硬件支持副总裁 \_ 模式 \_ TV \_ 播放，则同时设置此位。

-   将 **dwTVStandard** 设置为 "副总裁 \_ 电视 \_ 标准 \_ WIN \_ VGA"。

-   在 **dwAvailableTVStandard**中，设置代表电视连接器支持的电视标准的所有位。

-   对于 **dwFlags** 中设置的所有标志 (除了已 \_ \_) 讨论的 vp 标志电视 \_ 模式和副总裁 \_ 标志 \_ tv STANDARD， \_ 请将值分配给 VIDEOPARAMETERS 结构的相应成员。

示例2：若要启用电视输出，调用方 (不是微型端口驱动程序) 应执行以下操作：

-   在 **dwFlags**中，设置 vp \_ 标志 \_ 电视 \_ 模式和 vp \_ 标志 \_ 电视 \_ 标准。 清除所有其他标志。

-   将 **dwMode** 设置为副总裁 \_ 模式 \_ WIN \_ 图形或副总裁 \_ 模式 \_ TV \_ 播放。 不要设置这两个位。

-   将 **dwTvStandard** 设置为所需的标准 (例如副总裁 \_ TV \_ standard \_ NTSC \_ M) 。 不要在 **dwTvStandard**中设置任何其他位。

示例3：若要禁用电视输出，调用方不 (微型端口驱动程序) 应执行以下操作：

-   在 **dwFlags**中，设置 vp \_ 标志 \_ 电视 \_ 模式和 vp \_ 标志 \_ 电视 \_ 标准。 清除所有其他标志。

-   将 **dwMode** 设置为0。

-   在 **dwTvStandard**中，设置副总裁 \_ 电视 \_ 标准 \_ WIN \_ VGA。 清除 **dwTvStandard**中的所有其他位。

 

