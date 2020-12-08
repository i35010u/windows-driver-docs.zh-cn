---
title: DXVA-HD DDI
description: DXVA-HD DDI
keywords:
- DXVA-HD DDI WDK Windows 7 显示
- DXVA-HD DDI WDK Server 2008 R2 显示
- 高清晰视频 WDK Windows 7 显示，DXVA-HD DDI
- 高清晰视频 WDK Server 2008 R2 display，DXVA-HD DDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd6e427693de64a936cb96fdfe2d8a0f9d80046a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799724"
---
# <a name="dxva-hd-ddi"></a>DXVA-HD DDI


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

DXVA DDI 是 [Direct3D 版本 9 ddi](/windows-hardware/drivers/ddi/d3dumddi/index) 的扩展，用于处理高清晰度视频的处理。 DXVA DDI 包含以下入口点：

-   Direct3D 运行时使用以下 [**D3DDDICAPS \_ 类型**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_d3dddicaps_type) 值来检索有关用户模式显示驱动程序支持的高清晰视频处理功能的信息。 运行时在 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的 **TYPE** 成员中设置这些 **D3DDDICAPS \_ 类型** 的值，在运行时调用 *GETCAPS* 时，驱动程序的 [**GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数的 *pData* 参数指向该函数。

    <span id="D3DDDICAPS_DXVAHD_GETVPDEVCAPS"></span><span id="d3dddicaps_dxvahd_getvpdevcaps"></span>D3DDDICAPS \_ DXVAHD \_ GETVPDEVCAPS  
    该驱动程序提供了一个指针，用于显示解码设备 (的视频处理器功能的 [**DXVAHDDDI \_ VPDEVCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpdevcaps)结构，该结构是通过 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持的 **pInfo** 成员指向的 [**DXVAHDDDI \_ 设备 \_ DESC**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)结构中指定的。

    <span id="D3DDDICAPS_DXVAHD_GETVPOUTPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpoutputformats"></span>D3DDDICAPS \_ DXVAHD \_ GETVPOUTPUTFORMATS  
    驱动程序提供了 [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举类型的数组，这些类型表示解码设备 (的输出格式，该格式是由 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 的 **pInfo** 成员指向的 [**DXVAHDDDI \_ 设备 \_ DESC**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)结构中指定的。

    <span id="D3DDDICAPS_DXVAHD_GETVPINPUTFORMATS"></span><span id="d3dddicaps_dxvahd_getvpinputformats"></span>D3DDDICAPS \_ DXVAHD \_ GETVPINPUTFORMATS  
    驱动程序提供 [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)枚举类型的数组，这些类型表示解码设备 (的输入格式，该格式是由 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 的 **pInfo** 成员指向的 [**DXVAHDDDI \_ 设备 \_ DESC**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)结构中指定的。

    <span id="D3DDDICAPS_DXVAHD_GETVPCAPS"></span><span id="d3dddicaps_dxvahd_getvpcaps"></span>D3DDDICAPS \_ DXVAHD \_ GETVPCAPS  
    驱动程序为每个视频处理器的功能提供了一个 [**DXVAHDDDI \_ VPCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_vpcaps)结构的数组，这些功能是解码设备 (的，它是在 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持的 **pInfo** 成员指向的 [**DXVAHDDDI \_ 设备 \_ DESC**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_device_desc)结构中指定的。

    <span id="D3DDDICAPS_DXVAHD_GETVPCUSTOMRATES"></span><span id="d3dddicaps_dxvahd_getvpcustomrates"></span>D3DDDICAPS \_ DXVAHD \_ GETVPCUSTOMRATES  
    驱动程序为自定义帧速率提供 [**DXVAHDDDI \_ 自定义 \_ 速率 \_ 数据**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_custom_rate_data)结构的数组，视频处理器 (此结构由 \_ [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持的 **pInfo** 成员所指的 CONST GUID 指定。

    <span id="D3DDDICAPS_DXVAHD_GETVPFILTERRANGE"></span><span id="d3dddicaps_dxvahd_getvpfilterrange"></span>D3DDDICAPS \_ DXVAHD \_ GETVPFILTERRANGE  
    驱动程序提供了一个指针，指向 (筛选器范围的筛选器 [**\_ \_ 范围 \_ 数据**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvahdddi_filter_range_data)结构，该结构由 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)) 支持的 **pInfo** 成员指向的 [**DXVAHDDDI \_ 筛选器**](/windows-hardware/drivers/ddi/d3dumddi/ne-d3dumddi-_dxvahdddi_filter)枚举值指定。

-   [**CreateVideoProcessor**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_createvideoprocessor)函数将创建可处理高清晰度视频的视频处理器。

-   [**SetVideoProcessBltState**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessbltstate)函数为视频处理器设置位块传输 (bitblt) 的状态。

-   [**GetVideoProcessBltStatePrivate**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessbltstateprivate)函数检索视频处理器专用 bitblt 的状态数据。

-   [**SetVideoProcessStreamState**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_setvideoprocessstreamstate)函数为视频处理器设置流的状态。

-   [**GetVideoProcessStreamStatePrivate**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_getvideoprocessstreamstateprivate)函数检索视频处理器的专用流状态数据。

-   [**VideoProcessBltHD**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_videoprocessblthd)函数处理视频输入流，并将其组合到一个输出图面上。

-   [**DestroyVideoProcessor**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_dxvahd_destroyvideoprocessor)函数释放先前创建的视频处理器的资源。

 

