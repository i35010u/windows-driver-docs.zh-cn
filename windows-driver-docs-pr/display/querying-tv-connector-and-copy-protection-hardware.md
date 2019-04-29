---
title: 查询电视连接器和复制保护硬件
description: 查询电视连接器和复制保护硬件
ms.assetid: 7812a3ba-42f1-4872-bfe8-08933802f0c1
keywords:
- 电视连接器 WDK 微型端口
- 复制保护 WDK 视频的微型端口，查询
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9cf18cf5d08535313b9d5bd990595ffb6ae6bb78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392645"
---
# <a name="querying-tv-connector-and-copy-protection-hardware"></a>查询电视连接器和复制保护硬件


## <span id="ddk_querying_tv_connector_and_copy_protection_hardware_gg"></span><span id="DDK_QUERYING_TV_CONNECTOR_AND_COPY_PROTECTION_HARDWARE_GG"></span>


有一个电视连接器的适配器的微型端口驱动程序必须处理[ **IOCTL\_视频\_处理\_VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff567805)请求在其[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)函数。 IOCTL 请求时 IOCTL\_视频\_处理\_VIDEOPARAMETERS， **InputBuffer**隶属[**视频\_请求\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff570547)结构，指向[ **VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff570173)结构。 **DwCommand**该 VIDEOPARAMETERS 结构的成员指定微型端口驱动程序是否必须提供有关电视连接器的信息 (副总裁\_命令\_获取) 或将指定的设置应用到电视连接器 (副总裁\_命令\_设置)。

当**dwCommand** VIDEOPARAMETERS 结构中的成员是副总裁\_命令\_GET、 微型端口驱动程序必须执行以下操作：

-   验证是否**Guid** VIDEOPARAMETERS 结构中的成员。

-   电视连接器支持，每个功能中设置相应标志**dwFlags** VIDEOPARAMETERS 结构中的成员。

-   对于每个标记设置**dwFlags**成员，以指示功能以及与该标记关联的当前设置的相应 VIDEOPARAMETERS 结构成员分配值。 请参阅[ **VIDEOPARAMETERS** ](https://msdn.microsoft.com/library/windows/hardware/ff570173)对应于给定的标记的结构成员的列表的参考页。

**DwMode** VIDEOPARAMETERS 结构中的成员指定电视是否输出进行了优化的视频播放或显示 Windows 桌面。 值为视频\_模式下\_电视\_播放指定电视输出针对视频播放优化 （即，禁用闪烁筛选器和电视机之间启用）。 值为视频\_模式下\_赢取\_图形指定电视输出适用于 Windows 的图形 （也就是说，启用了最大闪烁筛选器和电视机之间已禁用）。

在响应副总裁\_命令\_GET、 微型端口驱动程序必须设置副总裁\_标志\_电视\_中的模式标志**dwFlags** ，必须设置副总裁\_模式\_赢得\_图形中的位**dwAvailableModes**。 设置副总裁\_模式下\_电视\_播放位**dwAvailableModes**是可选的。 此外，微型端口驱动程序必须设置副总裁\_标志\_最大\_不成比例中的标志**dwFlags**必须将值分配给相应 VIDEOPARAMETERS 结构的成员。

响应副总裁\_命令\_获取，如果电视输出当前已禁用，微型端口驱动程序应设置**dwMode**为 0，设置**dwTVStandard**到副总裁\_标准\_赢得\_VGA，并设置**dwAvailableTVStandard**到副总裁\_标准\_赢取\_VGA。

示例 1：适配器支持的电视输出，当前已禁用。 微型端口驱动程序必须执行以下操作以响应副总裁\_命令\_获取：

-   在中**dwFlags**，设置副总裁\_标志\_电视\_模式下，副总裁\_标志\_电视\_标准，以及所有其他标记，表示支持的电视功能连接器。

-   设置**dwMode**为 0。

-   在中**dwAvailableModes**，设置副总裁\_模式\_赢取\_图形。 如果硬件支持副总裁\_模式下\_电视\_播放，集还位。

-   设置**dwTVStandard**到副总裁\_电视\_标准\_赢取\_VGA。

-   在中**dwAvailableTVStandard**，将表示支持的电视连接器的电视标准的所有位都设置。

-   中的所有标志都设置为**dwFlags** (以外副总裁\_标志\_电视\_模式和副总裁\_标志\_电视\_标准，已经讨论过)，将分配到 VIDEOPARAMETERS 结构的对应成员的值。

示例 2：若要启用电视输出，调用方 （而不是微型端口驱动程序） 应执行以下操作：

-   在中**dwFlags**，设置副总裁\_标志\_电视\_模式和副总裁\_标志\_电视\_标准。 清除所有其他标志。

-   设置**dwMode**到任一副总裁\_模式\_赢取\_图形或副总裁\_模式\_电视\_播放。 未设置两个位。

-   设置**dwTvStandard**所需的标准 (例如副总裁\_电视\_标准\_NTSC\_M)。 中未设置任何其他位**dwTvStandard**。

示例 3：若要禁用电视输出，调用方 （而不是微型端口驱动程序） 应执行以下操作：

-   在中**dwFlags**，设置副总裁\_标志\_电视\_模式和副总裁\_标志\_电视\_标准。 清除所有其他标志。

-   设置**dwMode**为 0。

-   在中**dwTvStandard**，设置副总裁\_电视\_标准\_赢取\_VGA。 清除所有其他位**dwTvStandard**。

 

 





