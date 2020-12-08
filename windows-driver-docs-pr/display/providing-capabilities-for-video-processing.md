---
title: 提供视频处理功能
description: 提供视频处理功能
keywords:
- 视频处理 WDK DirectX VA，请求类型提供的功能
- D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT
- D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS
- D3DDDICAPS_GETVIDEOPROCESSORCAPS
- D3DDDICAPS_GETPROCAMPRANGE
- D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT
- D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS
- D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT
- D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS
- D3DDDICAPS_FILTERPROPERTYRANGE
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 768bd7d336bc0a39b170b59b94589cbb41eb3064
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792925"
---
# <a name="providing-capabilities-for-video-processing"></a>提供视频处理功能


调用 [**GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数时，用户模式显示驱动程序将根据请求类型提供以下视频处理功能，该请求类型在 *pData* 参数指向) 的 [**D3DDDIARG \_ GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的 **type** 成员中指定 (：

<span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_request_types"></span><span id="d3dddicaps_getvideoprocessordeviceguidcount_and_d3dddicaps_getvideoprocessordeviceguids_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_REQUEST_TYPES"></span>D3DDDICAPS \_ GETVIDEOPROCESSORDEVICEGUIDCOUNT 和 D3DDDICAPS \_ GETVIDEOPROCESSORDEVICEGUIDS 请求类型  
用户模式显示驱动程序返回其支持用于视频处理的以下 Guid 的编号和列表。 Microsoft Direct3D runtime 为要在 D3DDDIARG GETCAPS 的 **pInfo** 成员指向的变量中处理的特定视频流指定 [**DXVADDI \_ VIDEODESC**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videodesc)结构 \_ 。 运行时首先请求支持的 Guid 的数目，并请求提供支持的 Guid 列表的请求。

```cpp
DEFINE_GUID(DXVADDI_VideoProcProgressiveDevice,  0x5a54a0c9,0xc7ec,0x4bd9,0x8e,0xde,0xf3,0xc7,0x5d,0xc4,0x39,0x3b);
DEFINE_GUID(DXVADDI_VideoProcBobDevice,  0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
```

<span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_request_type"></span><span id="d3dddicaps_getvideoprocessorcaps_request_type"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_REQUEST_TYPE"></span>D3DDDICAPS \_ GETVIDEOPROCESSORCAPS 请求类型  
用户模式显示驱动程序支持的每个视频处理器模式可以具有独特的功能。 用户模式显示驱动程序在 \_ 传递 D3DDDICAPS GETVIDEOPROCESSORCAPS 请求类型时返回这些功能。 Direct3D 运行时为视频处理模式指定 [**DXVADDI \_ VIDEOPROCESSORINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)结构，以便在 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)的 **pInfo** 成员指向的变量中检索的功能。 用户模式显示驱动程序将 [**DXVADDI \_ VIDEOPROCESSORCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorcaps) 结构中的视频处理模式的功能返回到 D3DDDIARG GETCAPS 的 **pData** 成员指向的 \_ 位置。

<span id="D3DDDICAPS_GETPROCAMPRANGE_request_type_"></span><span id="d3dddicaps_getprocamprange_request_type_"></span><span id="D3DDDICAPS_GETPROCAMPRANGE_REQUEST_TYPE_"></span>D3DDDICAPS \_ GETPROCAMPRANGE 请求类型   
用户模式显示驱动程序返回指向 [**DXVADDI \_ VALUERANGE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_valuerange) 结构的指针，该结构包含特定视频流上特定 ProcAmp 控件属性的允许值范围。 Direct3D 运行时在 D3DDDIARG GETCAPS 的 **pInfo** 成员指向的变量中，为特定视频流上的 ProcAmp 控件属性指定 [**DXVADDI \_ QUERYPROCAMPINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_queryprocampinput)结构 \_ 。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtformatcount_and_d3dddicaps_getvideoprocessorrtformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_REQUEST_TYPES"></span>D3DDDICAPS \_ GETVIDEOPROCESSORRTFORMATCOUNT 和 D3DDDICAPS \_ GETVIDEOPROCESSORRTFORMATS 请求类型  
用户模式显示驱动程序返回数字以及它支持的特定视频处理模式的呈现器目标格式列表。 Direct3D 运行时为 D3DDDIARG GETCAPS 的 **pInfo** 成员指向的变量中的视频处理器模式指定 [**DXVADDI \_ VIDEOPROCESSORINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)结构 \_ 。 用户模式显示驱动程序返回其在 D3DDDIARG GETCAPS 的 **pData** 成员指定的 [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)类型值的数组中支持的呈现目标格式 \_ 。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtsubstreamformatcount_and_d3dddicaps_getvideoprocessorrtsubstreamformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_REQUEST_TYPES"></span>D3DDDICAPS \_ GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT 和 D3DDDICAPS \_ GETVIDEOPROCESSORRTSUBSTREAMFORMATS 请求类型  
用户模式显示驱动程序将返回数字以及它支持的特定视频处理模式的子流格式列表。 Direct3D 运行时为 D3DDDIARG GETCAPS 的 **pInfo** 成员指向的变量中的视频处理器模式指定 [**DXVADDI \_ VIDEOPROCESSORINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_videoprocessorinput)结构 \_ 。 用户模式显示驱动程序返回 D3DDDIARG GETCAPS 的 **pData** 成员指定的 [**D3DDDIFORMAT**](/windows-hardware/drivers/ddi/d3dukmdt/ne-d3dukmdt-_d3dddiformat)类型值数组中所支持的子流格式 \_ 。

<span id="D3DDDICAPS_FILTERPROPERTYRANGE_request_type_"></span><span id="d3dddicaps_filterpropertyrange_request_type_"></span><span id="D3DDDICAPS_FILTERPROPERTYRANGE_REQUEST_TYPE_"></span>D3DDDICAPS \_ FILTERPROPERTYRANGE 请求类型   
用户模式显示驱动程序返回指向 [**DXVADDI \_ VALUERANGE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_valuerange) 结构的指针，该结构包含在 \_ 传递 D3DDDICAPS FILTERPROPERTYRANGE 请求类型时特定视频流的特定筛选器设置允许的值范围。 Direct3D 运行时为 D3DDDIARG GETCAPS 的 **pInfo** 成员指向的变量中的特定视频流指定筛选器设置的 [**DXVADDI \_ QUERYFILTERPROPERTYRANGEINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_queryfilterpropertyrangeinput)结构 \_ 。

 

