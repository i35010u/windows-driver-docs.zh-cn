---
title: 创建压缩缓冲区和解码渲染器目标
description: 创建压缩缓冲区和解码渲染器目标
ms.assetid: 4d386b72-24d9-424b-8d48-7eaf75aab76c
keywords:
- 视频解码 WDK DirectX VA，呈现器目标
- 解码视频 WDK DirectX VA，呈现器目标
- 视频解码 WDK DirectX VA，压缩缓冲区
- 解码视频 WDK DirectX VA，压缩的缓冲区
- 压缩的缓冲区 WDK DirectX VA
- 缓冲 WDK DirectX VA
- 呈现器目标 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b274e4a483834275bdc8b4030ec1e8224fff5f8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370201"
---
# <a name="creating-compressed-buffers-and-decode-render-targets"></a>创建压缩缓冲区和解码渲染器目标


Microsoft Direct3D 运行时将调用用户模式显示驱动程序[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数来创建压缩的缓冲区，并呈现器目标用于解码。

每个压缩的缓冲区类型都有其自己图面上的格式，以及指示运行时创建的图面包含压缩的缓冲区的信息，用于加速的视频解码的特殊标志。 用户模式显示驱动程序确定要创建压缩的缓冲区，如果**DecodeCompressedBuffer**中的位域标志**标志**的成员[ **D3DDDIARG\_CREATERESOURCE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的*pResource*参数[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)设置到的点。 用户模式显示驱动程序确定压缩缓冲区中的格式值创建的类型**格式**D3DDDIARG 成员\_CREATERESOURCE。 定义以下格式：

```cpp
D3DDDIFMT_PICTUREPARAMSDATA       = 150
D3DDDIFMT_MACROBLOCKDATA          = 151
D3DDDIFMT_RESIDUALDIFFERENCEDATA  = 152
D3DDDIFMT_DEBLOCKINGDATA          = 153
D3DDDIFMT_INVERSEQUANTIZATIONDATA = 154
D3DDDIFMT_SLICECONTROLDATA        = 155
D3DDDIFMT_BITSTREAMDATA           = 156
```

Direct3D 运行时创建每个解码呈现器目标独立用户模式显示驱动程序的调用中[ **CreateResource** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)函数。 每个目标是作为单个资源的子资源索引引用。 用户模式显示驱动程序确定创建解码呈现器目标，如果**DecodeRenderTarget**中的位域标志**标志**D3DDDIARG 成员\_CREATERESOURCE 设置。

 

 





