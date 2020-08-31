---
title: 创建压缩缓冲区和解码渲染器目标
description: 创建压缩缓冲区和解码渲染器目标
ms.assetid: 4d386b72-24d9-424b-8d48-7eaf75aab76c
keywords:
- 视频解码 WDK DirectX VA，呈现目标
- 解码视频 WDK DirectX VA，呈现目标
- 视频解码 WDK DirectX VA，压缩缓冲区
- 解码视频 WDK DirectX VA，压缩缓冲区
- 压缩的缓冲区 WDK DirectX VA
- 缓冲 WDK DirectX VA
- 呈现目标 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8854a6bceaabe7795d948c6f15b751542bfaeba4
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063156"
---
# <a name="creating-compressed-buffers-and-decode-render-targets"></a>创建压缩缓冲区和解码渲染器目标


Microsoft Direct3D runtime 调用用户模式显示驱动程序的 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 函数，以创建压缩缓冲区和呈现目标进行解码。

每个压缩的缓冲区类型都有其自己的表面格式和一个特殊标志，该标志指示运行时创建的图面包含用于加速视频解码的压缩缓冲信息。 用户模式显示驱动程序确定在[**D3DDDIARG \_ CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dukmdt/ns-d3dukmdt-_d3dddiarg_createresource)结构的**Flags**成员中**DecodeCompressedBuffer**位域标志设置为[**CREATERESOURCE**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource)指向的*pResource*参数时，创建压缩缓冲区。 用户模式显示驱动程序通过 D3DDDIARG CREATERESOURCE 的 **format** 成员确定格式值创建的压缩缓冲区的类型 \_ 。 定义以下格式：

```cpp
D3DDDIFMT_PICTUREPARAMSDATA       = 150
D3DDDIFMT_MACROBLOCKDATA          = 151
D3DDDIFMT_RESIDUALDIFFERENCEDATA  = 152
D3DDDIFMT_DEBLOCKINGDATA          = 153
D3DDDIFMT_INVERSEQUANTIZATIONDATA = 154
D3DDDIFMT_SLICECONTROLDATA        = 155
D3DDDIFMT_BITSTREAMDATA           = 156
```

Direct3D 运行时在对用户模式显示驱动程序的 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 函数的调用中单独创建每个解码呈现器目标。 每个目标都作为单个资源的 subresource 索引进行引用。 如果设置了 D3DDDIARG CREATERESOURCE**标志**成员的**DecodeRenderTarget**位域标志，则用户模式显示驱动程序将确定创建解码呈现器目标 \_ 。

 

