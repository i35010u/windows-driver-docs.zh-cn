---
title: DXVA-HD DDI
description: DXVA-HD DDI
ms.assetid: 8b44a5b7-dc86-46eb-83e1-39caa72ffa34
keywords:
- DXVA-HD DDI WDK Windows 7 显示
- DXVA-HD DDI WDK Server 2008 R2 显示
- 高清晰视频 WDK Windows 7 显示，DXVA-HD DDI
- 高清晰视频 WDK Server 2008 R2 display，DXVA-HD DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b5a763b0978588c28a2e9e4b8e65096e89c70d8e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838961"
---
# <a name="dxva-hd-ddi"></a>DXVA-HD DDI


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

DXVA DDI 是[Direct3D 版本 9 ddi](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/index)的扩展，用于处理高清晰度视频的处理。 DXVA DDI 包含以下入口点：

-   Direct3D 运行时使用以下[**D3DDDICAPS\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type)值来检索有关用户模式显示驱动程序支持的高清晰视频处理功能的信息。 运行时将这些**D3DDDICAPS 设置\_类型** [ **\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的**类型**成员中的值，在运行时调用时，驱动程序的[**GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数的*pData*参数指向*GetCaps*。

    <span id="D3DDDICAPS_DXVAHD_GETVPDEVCAPS"></span><span id="d3dddicaps_dxvahd_getvpdevcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPDEVCAPS  
    该驱动程序提供了一个指针，用于显示解码设备（在[**DXVAHDDDI\_\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)中指定的视频处理器功能的[**DXVAHDDDI\_VPDEVCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)结构。 [**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)）的 pInfo 成员支持。

    <span id="D3DDDICAPS_DXVAHD_GETVPOUTPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpoutputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPOUTPUTFORMATS  
    驱动程序提供了[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举类型的数组，这些类型表示解码设备（在[**DXVAHDDDI\_\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)中指定的解码格式）的输出格式。 **pInfo**成员指向的[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)）。

    <span id="D3DDDICAPS_DXVAHD_GETVPINPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpinputformats"></span>D3DDDICAPS\_DXVAHD\_GETVPINPUTFORMATS  
    驱动程序提供了[**D3DDDIFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举类型的数组，这些类型表示解码设备的输入格式（在[**DXVAHDDDI\_\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)中指定的[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)）。

    <span id="D3DDDICAPS_DXVAHD_GETVPCAPS"></span><span id="d3dddicaps_dxvahd_getvpcaps"></span>D3DDDICAPS\_DXVAHD\_GETVPCAPS  
    驱动程序为每个视频处理器的功能提供了一个[**DXVAHDDDI\_VPCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpcaps)结构的数组，该解码设备（在[**DXVAHDDDI\_设备**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)中指定，\_[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)）的**pInfo**成员支持。

    <span id="D3DDDICAPS_DXVAHD_GETVPCUSTOMRATES"></span><span id="d3dddicaps_dxvahd_getvpcustomrates"></span>D3DDDICAPS\_DXVAHD\_GETVPCUSTOMRATES  
    驱动程序为自定义的帧速率提供了一组[**DXVAHDDDI\_自定义\_\_速率的数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_custom_rate_data)结构，这些数据结构用于视频处理器（\_由**pInfo**成员[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)）支持。

    <span id="D3DDDICAPS_DXVAHD_GETVPFILTERRANGE"></span><span id="d3dddicaps_dxvahd_getvpfilterrange"></span>D3DDDICAPS\_DXVAHD\_GETVPFILTERRANGE  
    驱动程序提供指向[**DXVAHDDDI\_筛选器的指针\_范围\_数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)结构，该范围是筛选器（由**PInfo**指向的[**DXVAHDDDI\_筛选器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_filter)枚举值指定）。[**D3DDDIARG\_GETCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)）的成员支持。

-   [**CreateVideoProcessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)函数将创建可处理高清晰度视频的视频处理器。

-   [**SetVideoProcessBltState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessbltstate)函数设置视频处理器的位块传输（bitblt）的状态。

-   [**GetVideoProcessBltStatePrivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)函数检索视频处理器专用 bitblt 的状态数据。

-   [**SetVideoProcessStreamState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessstreamstate)函数为视频处理器设置流的状态。

-   [**GetVideoProcessStreamStatePrivate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)函数检索视频处理器的专用流状态数据。

-   [**VideoProcessBltHD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_videoprocessblthd)函数处理视频输入流，并将其组合到一个输出图面上。

-   [**DestroyVideoProcessor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_destroyvideoprocessor)函数释放先前创建的视频处理器的资源。

 

 





