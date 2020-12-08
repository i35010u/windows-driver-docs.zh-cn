---
title: 提供视频解码功能
description: 提供视频解码功能
keywords:
- 视频解码 WDK DirectX VA，按请求类型提供的功能
- 解码视频 WDK DirectX VA，按请求类型提供的功能
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
ms.openlocfilehash: 9f82049967a25b5cae34675deb3c5796a513f963
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792937"
---
# <a name="providing-capabilities-for-video-decoding"></a>提供视频解码功能


调用 [**GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_getcaps)函数时，用户模式显示驱动程序会根据请求类型提供以下功能，这些功能可用于在 *GetCaps* 函数的 *PData* 参数指向) 的 [**D3DDDIARG \_ GetCaps**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)结构的 **type** 成员中指定的请求类型 (：

<span id="D3DDDICAPS_GETDECODEGUIDCOUNT_and_D3DDDICAPS_GETDECODEGUIDS_request_types"></span><span id="d3dddicaps_getdecodeguidcount_and_d3dddicaps_getdecodeguids_request_types"></span><span id="D3DDDICAPS_GETDECODEGUIDCOUNT_AND_D3DDDICAPS_GETDECODEGUIDS_REQUEST_TYPES"></span>D3DDDICAPS \_ GETDECODEGUIDCOUNT 和 D3DDDICAPS \_ GETDECODEGUIDS 请求类型  
用户模式显示驱动程序返回其支持的、视频加速 (VA) 解码的以下 Guid 的列表。 Microsoft Direct3D runtime 首先会请求 Guid 数量，然后请求提供支持的 Guid 列表的请求。

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

<span id="D3DDDICAPS_GETDECODERTFORMATCOUNT_and_D3DDDICAPS_GETDECODERTFORMATS_request_types"></span><span id="d3dddicaps_getdecodertformatcount_and_d3dddicaps_getdecodertformats_request_types"></span><span id="D3DDDICAPS_GETDECODERTFORMATCOUNT_AND_D3DDDICAPS_GETDECODERTFORMATS_REQUEST_TYPES"></span>D3DDDICAPS \_ GETDECODERTFORMATCOUNT 和 D3DDDICAPS \_ GETDECODERTFORMATS 请求类型  
用户模式显示驱动程序将返回该数字以及它支持用于特定 DirectX VA 解码类型的呈现器目标格式列表。 Direct3D 运行时在 [**D3DDDIARG \_ GETCAPS**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_getcaps)指向的 **pInfo** 成员变量中指定特定 DIRECTX VA 解码类型的 GUID。

<span id="D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT_and_D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO_request_types"></span><span id="d3dddicaps_getdecodecompressedbufferinfocount_and_d3dddicaps_getdecodecompressedbufferinfo_request_types"></span><span id="D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFOCOUNT_AND_D3DDDICAPS_GETDECODECOMPRESSEDBUFFERINFO_REQUEST_TYPES"></span>D3DDDICAPS \_ GETDECODECOMPRESSEDBUFFERINFOCOUNT 和 D3DDDICAPS \_ GETDECODECOMPRESSEDBUFFERINFO 请求类型  
用户模式显示驱动程序返回有关加快视频解码所需的压缩缓冲区类型的数量和信息。 Direct3D 运行时为 D3DDDIARG GETCAPS 的 **pInfo** 成员指向的变量中的特定 DirectX VA 解码类型指定 [**DXVADDI \_ DECODEINPUT**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodeinput)结构 \_ 。 用户模式显示驱动程序返回与 D3DDDIARG GETCAPS 的 **pData** 成员指定的 [**DXVADDI \_ DECODEBUFFERINFO**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferinfo)结构数组中的压缩缓冲区类型有关的信息 \_ 。

<span id="D3DDDICAPS_GETDECODECONFIGURATIONCOUNT_and_D3DDDICAPS_GETDECODECONFIGURATIONS_request_types"></span><span id="d3dddicaps_getdecodeconfigurationcount_and_d3dddicaps_getdecodeconfigurations_request_types"></span><span id="D3DDDICAPS_GETDECODECONFIGURATIONCOUNT_AND_D3DDDICAPS_GETDECODECONFIGURATIONS_REQUEST_TYPES"></span>D3DDDICAPS \_ GETDECODECONFIGURATIONCOUNT 和 D3DDDICAPS \_ GETDECODECONFIGURATIONS 请求类型  
用户模式显示驱动程序返回其支持的针对特定 DirectX VA 解码类型的加速解码配置的列表。 Direct3D 运行时 \_ 为 D3DDDIARG GETCAPS 的 **pInfo** 成员指向的变量中的特定 DirectX VA 解码类型指定 DXVADDI DECODEINPUT 结构 \_ 。 用户模式显示驱动程序在 D3DDDIARG GETCAPS 的 **pData** 成员指定的 [**DXVADDI \_ CONFIGPICTUREDECODE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_configpicturedecode)结构的数组中返回加速解码配置 \_ 。

 

