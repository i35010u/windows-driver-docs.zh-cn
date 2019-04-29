---
title: 提供视频处理功能
description: 提供视频处理功能
ms.assetid: 27507971-1545-44d9-885a-295b9357bdfe
keywords:
- 视频处理 WDK DirectX VA，提供请求类型的功能
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
ms.openlocfilehash: 929caf5968958acfe0cc1645d060335e373e5830
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370159"
---
# <a name="providing-capabilities-for-video-processing"></a>提供视频处理功能


当其[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)调用函数，用户模式显示驱动程序提供以下基于请求类型的视频处理功能 (中指定**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)结构*pData*参数指向):

<span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_request_types"></span><span id="d3dddicaps_getvideoprocessordeviceguidcount_and_d3dddicaps_getvideoprocessordeviceguids_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORDEVICEGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORDEVICEGUIDCOUNT 和 D3DDDICAPS\_GETVIDEOPROCESSORDEVICEGUIDS 请求类型  
用户模式显示驱动程序返回数和它支持的视频处理以下 Guid 的列表。 Microsoft Direct3D 运行时指定[ **DXVADDI\_VIDEODESC** ](https://msdn.microsoft.com/library/windows/hardware/ff562944)结构来处理在变量中的特定视频流的**pInfo**成员 D3DDDIARG\_GETCAPS 指向。 在运行时首先请求支持 Guid 后, 跟一系列受支持的 Guid 的请求数。

```cpp
DEFINE_GUID(DXVADDI_VideoProcProgressiveDevice,  0x5a54a0c9,0xc7ec,0x4bd9,0x8e,0xde,0xf3,0xc7,0x5d,0xc4,0x39,0x3b);
DEFINE_GUID(DXVADDI_VideoProcBobDevice,  0x335aa36e,0x7884,0x43a4,0x9c,0x91,0x7f,0x87,0xfa,0xf3,0xe3,0x7e);
```

<span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_request_type"></span><span id="d3dddicaps_getvideoprocessorcaps_request_type"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORCAPS_REQUEST_TYPE"></span>D3DDDICAPS\_GETVIDEOPROCESSORCAPS 请求类型  
用户模式显示驱动程序支持每个视频处理器模式可具有独特的功能。 用户模式显示驱动程序返回这些功能时 D3DDDICAPS\_传递 GETVIDEOPROCESSORCAPS 请求类型。 Direct3D 运行时指定[ **DXVADDI\_VIDEOPROCESSORINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562956)若要检索的变量中的功能的视频处理模式的结构的**pInfo**的成员[ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)指向。 用户模式显示驱动程序返回中的视频处理模式的功能[ **DXVADDI\_VIDEOPROCESSORCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff562953)结构**pData**成员 D3DDDIARG\_GETCAPS 指向。

<span id="D3DDDICAPS_GETPROCAMPRANGE_request_type_"></span><span id="d3dddicaps_getprocamprange_request_type_"></span><span id="D3DDDICAPS_GETPROCAMPRANGE_REQUEST_TYPE_"></span>D3DDDICAPS\_GETPROCAMPRANGE 请求类型   
用户模式显示驱动程序将返回一个指向[ **DXVADDI\_VALUERANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff562939)结构，它包含范围的允许对特定的特定 ProcAmp 控件属性的值视频流。 Direct3D 运行时指定[ **DXVADDI\_QUERYPROCAMPINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562935)结构的变量中的特定视频流的 ProcAmp 控件属性的**pInfo** D3DDDIARG 成员\_GETCAPS 指向。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtformatcount_and_d3dddicaps_getvideoprocessorrtformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORRTFORMATCOUNT 和 D3DDDICAPS\_GETVIDEOPROCESSORRTFORMATS 请求类型  
用户模式显示驱动程序返回数字和列表的呈现目标格式，它支持的特定视频处理模式。 Direct3D 运行时指定[ **DXVADDI\_VIDEOPROCESSORINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562956)结构的变量中的视频处理器模式的**pInfo**的成员D3DDDIARG\_GETCAPS 指向。 用户模式显示驱动程序返回呈现它支持在一个数组中的目标格式[ **D3DDDIFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff544312)的类型化值**pData** D3DDDIARG 成员\_GETCAPS 指定。

<span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_and_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_request_types"></span><span id="d3dddicaps_getvideoprocessorrtsubstreamformatcount_and_d3dddicaps_getvideoprocessorrtsubstreamformats_request_types"></span><span id="D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT_AND_D3DDDICAPS_GETVIDEOPROCESSORRTSUBSTREAMFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETVIDEOPROCESSORRTSUBSTREAMFORMATCOUNT 和 D3DDDICAPS\_GETVIDEOPROCESSORRTSUBSTREAMFORMATS 请求类型  
用户模式显示驱动程序返回数和它支持的特定视频处理模式下的子流格式的列表。 Direct3D 运行时指定[ **DXVADDI\_VIDEOPROCESSORINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562956)结构的变量中的视频处理器模式的**pInfo**的成员D3DDDIARG\_GETCAPS 指向。 用户模式显示驱动程序将返回它支持在一个数组中的子流格式[ **D3DDDIFORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff544312)的类型化值**pData** D3DDDIARG 成员\_GETCAPS 指定。

<span id="D3DDDICAPS_FILTERPROPERTYRANGE_request_type_"></span><span id="d3dddicaps_filterpropertyrange_request_type_"></span><span id="D3DDDICAPS_FILTERPROPERTYRANGE_REQUEST_TYPE_"></span>D3DDDICAPS\_FILTERPROPERTYRANGE 请求类型   
用户模式显示驱动程序将返回一个指向[ **DXVADDI\_VALUERANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff562939)结构，它包含范围的允许值的特定视频流上的特定筛选器设置当 D3DDDICAPS\_传递 FILTERPROPERTYRANGE 请求类型。 Direct3D 运行时指定[ **DXVADDI\_QUERYFILTERPROPERTYRANGEINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562930)结构用于在变量中的特定视频流上的筛选器设置的**pInfo** D3DDDIARG 成员\_GETCAPS 指向。

 

 





