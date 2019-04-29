---
title: 提供视频解码功能
description: 提供视频解码功能
ms.assetid: bffcc0da-7b1a-4f70-98f5-4841c8df9f12
keywords:
- 视频解码 WDK DirectX VA，功能提供每个请求类型
- 解码视频 WDK DirectX va，因此每个请求类型提供的功能
- D3DDDICAPS_GETDECODEGUIDCOUNT
- D3DDDICAPS_GETDECODEGUIDS
- D3DDDICAPS_GETDECODERTFORMATCOUNT
- D3DDDICAPS_GETDECODERTFORMATS
- D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT
- D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO
- D3DDDICAPS_GETDECODECONFIGURATIONCOUNT
- D3DDDICAPS_GETDECODECONFIGURATIONS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ed25b655066e33c770f76b278498be1fe4da608
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383866"
---
# <a name="providing-capabilities-for-video-decoding"></a>提供视频解码功能


当其[ **GetCaps** ](https://msdn.microsoft.com/library/windows/hardware/ff566762)调用函数，用户模式显示驱动程序提供以下功能的视频解码基于请求类型 (中指定**类型**的成员[ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)结构*GetCaps*函数的*pData*参数指向):

<span id="D3DDDICAPS_GETDECODEGUIDCOUNT_and_D3DDDICAPS_GETDECODEGUIDS_request_types"></span><span id="d3dddicaps_getdecodeguidcount_and_d3dddicaps_getdecodeguids_request_types"></span><span id="D3DDDICAPS_GETDECODEGUIDCOUNT_AND_D3DDDICAPS_GETDECODEGUIDS_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODEGUIDCOUNT 和 D3DDDICAPS\_GETDECODEGUIDS 请求类型  
用户模式显示驱动程序返回数和它支持用于视频加速 (VA) 解码的以下 Guid 的列表。 Microsoft Direct3D 运行时第一次请求后发出请求的支持的 Guid 的列表的 Guid 数目。

```cpp
DEFINE_GUID(DXVADDI_ModeMPEG2_MoComp, 0xe6a9f44b, 0x61b0, 0x4563,0x9e,0xa4,0x63,0xd2,0xa3,0xc6,0xfe,0x66);
DEFINE_GUID(DXVADDI_ModeMPEG2_IDCT,   0xbf22ad00, 0x03ea, 0x4690,0x80,0x77,0x47,0x33,0x46,0x20,0x9b,0x7e);
DEFINE_GUID(DXVADDI_ModeMPEG2_VLD,    0xee27417f, 0x5e28, 0x4e65,0xbe,0xea,0x1d,0x26,0xb5,0x08,0xad,0xc9);

DEFINE_GUID(DXVADDI_ModeH264_A,  0x1b81be64, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_B,  0x1b81be65, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_C,  0x1b81be66, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_D,  0x1b81be67, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_E,  0x1b81be68, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeH264_F,  0x1b81be69, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

DEFINE_GUID(DXVADDI_ModeWMV8_A,  0x1b81be80, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeWMV8_B,  0x1b81be81, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

DEFINE_GUID(DXVADDI_ModeWMV9_A,  0x1b81be90, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeWMV9_B,  0x1b81be91, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeWMV9_C,  0x1b81be94, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

DEFINE_GUID(DXVADDI_ModeVC1_A,   0x1b81beA0, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeVC1_B,   0x1b81beA1, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeVC1_C,   0x1b81beA2, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);
DEFINE_GUID(DXVADDI_ModeVC1_D,   0x1b81beA3, 0xa0c7, 0x11d3,0xb9,0x84,0x00,0xc0,0x4f,0x2e,0x73,0xc5);

#define DXVADDI_ModeMPEG2_MOCOMP  DXVADDI_ModeMPEG2_MoComp

#define DXVADDI_ModeWMV8_PostProc  DXVADDI_ModeWMV8_A
#define DXVADDI_ModeWMV8_MoComp  DXVADDI_ModeWMV8_B

#define DXVADDI_ModeWMV9_PostProc  DXVADDI_ModeWMV9_A
#define DXVADDI_ModeWMV9_MoComp  DXVADDI_ModeWMV9_B
#define DXVADDI_ModeWMV9_IDCT  DXVADDI_ModeWMV9_C

#define DXVADDI_ModeVC1_PostProc  DXVADDI_ModeVC1_A
#define DXVADDI_ModeVC1_MoComp  DXVADDI_ModeVC1_B
#define DXVADDI_ModeVC1_IDCT  DXVADDI_ModeVC1_C
#define DXVADDI_ModeVC1_VLD  DXVADDI_ModeVC1_D

#define DXVADDI_ModeH264_MoComp_NoFGT  DXVADDI_ModeH264_A
#define DXVADDI_ModeH264_MoComp_FGT  DXVADDI_ModeH264_B
#define DXVADDI_ModeH264_IDCT_NoFGT  DXVADDI_ModeH264_C
#define DXVADDI_ModeH264_IDCT_FGT  DXVADDI_ModeH264_D
#define DXVADDI_ModeH264_VLD_NoFGT  DXVADDI_ModeH264_E
#define DXVADDI_ModeH264_VLD_FGT  DXVADDI_ModeH264_F
```

<span id="D3DDDICAPS_GETDECODERTFORMATCOUNT_and_D3DDDICAPS_GETDECODERTFORMATS_request_types"></span><span id="d3dddicaps_getdecodertformatcount_and_d3dddicaps_getdecodertformats_request_types"></span><span id="D3DDDICAPS_GETDECODERTFORMATCOUNT_AND_D3DDDICAPS_GETDECODERTFORMATS_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODERTFORMATCOUNT 和 D3DDDICAPS\_GETDECODERTFORMATS 请求类型  
数字和列表的呈现目标格式，它支持特定的 DirectX VA 用户模式显示驱动程序返回对类型进行解码。 Direct3D 运行时为特定的 DirectX VA 解码类型的变量中指定的 GUID， **pInfo**的成员[ **D3DDDIARG\_GETCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff543148)点自。

<span id="D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT_and_D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO_request_types"></span><span id="d3dddicaps_getdecodecompressedbufferinfocount_and_d3dddicaps_getdecodecompressedbufferinfo_request_types"></span><span id="D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT_AND_D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODECOMPRESSEDBUFFERINFOCOUNT 和 D3DDDICAPS\_GETDECODECOMPRESSEDBUFFERINFO 请求类型  
用户模式显示驱动程序返回的数和加速视频解码所需的压缩的缓冲区类型信息。 Direct3D 运行时指定[ **DXVADDI\_DECODEINPUT** ](https://msdn.microsoft.com/library/windows/hardware/ff562903)结构特定的 DirectX VA 解码类型的变量中的**pInfo**的成员D3DDDIARG\_GETCAPS 指向。 用户模式显示驱动程序在一个数组中返回有关对压缩的缓冲区类型的信息[ **DXVADDI\_DECODEBUFFERINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff562900)结构的**pData** D3DDDIARG 成员\_GETCAPS 指定。

<span id="D3DDDICAPS_GETDECODECONFIGURATIONCOUNT_and_D3DDDICAPS_GETDECODECONFIGURATIONS_request_types"></span><span id="d3dddicaps_getdecodeconfigurationcount_and_d3dddicaps_getdecodeconfigurations_request_types"></span><span id="D3DDDICAPS_GETDECODECONFIGURATIONCOUNT_AND_D3DDDICAPS_GETDECODECONFIGURATIONS_REQUEST_TYPES"></span>D3DDDICAPS\_GETDECODECONFIGURATIONCOUNT 和 D3DDDICAPS\_GETDECODECONFIGURATIONS 请求类型  
用户模式显示驱动程序返回数和一系列加速解码为特定的 DirectX VA 解码类型支持的配置。 Direct3D 运行时指定 DXVADDI\_DECODEINPUT 结构特定的 DirectX VA 解码类型的变量中的**pInfo** D3DDDIARG 成员\_GETCAPS 指向。 加速用户模式显示驱动程序返回解码的数组中的配置[ **DXVADDI\_CONFIGPICTUREDECODE** ](https://msdn.microsoft.com/library/windows/hardware/ff562894)结构的**pData**D3DDDIARG 成员\_GETCAPS 指定。

 

 





