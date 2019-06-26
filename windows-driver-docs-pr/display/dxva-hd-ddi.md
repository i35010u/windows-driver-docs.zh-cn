---
title: DXVA-HD DDI
description: DXVA-HD DDI
ms.assetid: 8b44a5b7-dc86-46eb-83e1-39caa72ffa34
keywords:
- DXVA HD DDI WDK Windows 7 显示
- DXVA HD DDI WDK Server 2008 R2 显示
- 高清晰视频 WDK Windows 7 显示，DXVA HD DDI
- 高清晰视频 WDK Server 2008 R2 显示，DXVA HD DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8b31fe8ce47ddb1aadebaf80332fc0a1a9d9046
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375835"
---
# <a name="dxva-hd-ddi"></a>DXVA-HD DDI


本部分仅适用于 Windows 7 及更高版本、 和 Windows Server 2008 R2 和更高版本的 Windows 操作系统。

DXVA HD DDI 是扩展[Direct3D 版本 9 DDI](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/index)以处理高清晰度视频的处理。 DXVA HD DDI 包括以下入口点：

-   以下[ **D3DDDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_d3dddicaps_type)值由 Direct3D 运行时，用于检索有关用户模式下显示的高清晰视频处理功能的信息驱动程序支持。 运行时设置这些**D3DDDICAPS\_类型**中的值**类型**隶属[ **D3DDDIARG\_GETCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的*pData*驱动程序的参数[ **GetCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数运行时调用的时点*GetCaps*.

    <span id="D3DDDICAPS_DXVAHD_GETVPDEVCAPS"></span><span id="d3dddicaps_dxvahd_getvpdevcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPDEVCAPS  
    该驱动程序提供一个指针指向[ **DXVAHDDDI\_VPDEVCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)视频处理器功能的结构的解码设备 (在指定的[ **DXVAHDDDI\_设备\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)所指向的结构**pInfo**的成员[ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持。

    <span id="D3DDDICAPS_DXVAHD_GETVPOUTPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpoutputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPOUTPUTFORMATS  
    该驱动程序提供了一系列[ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)表示解码设备的输出格式的枚举类型 (中指定[ **DXVAHDDDI\_设备\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)指向的结构**pInfo**隶属[ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)).

    <span id="D3DDDICAPS_DXVAHD_GETVPINPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpinputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPINPUTFORMATS  
    该驱动程序提供了一系列[ **D3DDDIFORMAT** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ne-d3dukmdt-_d3dddiformat)表示解码设备的输入的格式的枚举类型 (中指定[ **DXVAHDDDI\_设备\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)指向的结构**pInfo**隶属[ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)).

    <span id="D3DDDICAPS_DXVAHD_GETVPCAPS"></span><span id="d3dddicaps_dxvahd_getvpcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPCAPS  
    驱动程序提供了一系列[ **DXVAHDDDI\_VPCAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_vpcaps)为每个视频的处理器功能的结构的解码设备 (在指定的[ **DXVAHDDDI\_设备\_DESC** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)所指向的结构**pInfo**隶属[ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持。

    <span id="D3DDDICAPS_DXVAHD_GETVPCUSTOMRATES"></span><span id="d3dddicaps_dxvahd_getvpcustomrates"></span>D3DDDICAPS\_DXVAHD\_GETVPCUSTOMRATES  
    该驱动程序提供了一系列[ **DXVAHDDDI\_自定义\_速率\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_custom_rate_data)结构为自定义的帧速率的视频处理器 (通过指定CONST\_所指向的 GUID **pInfo**的成员[ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持。

    <span id="D3DDDICAPS_DXVAHD_GETVPFILTERRANGE"></span><span id="d3dddicaps_dxvahd_getvpfilterrange"></span>D3DDDICAPS\_DXVAHD\_GETVPFILTERRANGE  
    驱动程序提供一个指针指向[ **DXVAHDDDI\_筛选器\_范围\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)结构范围的筛选器 (这指定[ **DXVAHDDDI\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ne-d3dumddi-_dxvahdddi_filter)枚举值，指向**pInfo**的成员[ **D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持。

-   [ **CreateVideoProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)函数将创建可处理高清晰视频的视频处理器。

-   [ **SetVideoProcessBltState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessbltstate)函数设置视频处理器的位块传输 (bitblt) 的状态。

-   [ **GetVideoProcessBltStatePrivate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)函数检索视频处理器专用 bitblt 的状态数据。

-   [ **SetVideoProcessStreamState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessstreamstate)函数适用于视频的处理器设置流的状态。

-   [ **GetVideoProcessStreamStatePrivate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)函数检索视频处理器的专用流状态数据。

-   [ **VideoProcessBltHD** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_videoprocessblthd)函数处理视频的输入的流，并将不复合到一个输出图面。

-   [ **DestroyVideoProcessor** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_destroyvideoprocessor)函数释放以前创建的视频处理器资源。

 

 





