---
title: 按像素将 Z 缓冲区升级到 32 位
description: 按像素将 Z 缓冲区升级到 32 位
ms.assetid: 6b7dddab-e154-44e8-a4e3-45bd706ed638
keywords:
- z 缓冲区 WDK DirectX 9.0
- 颜色缓冲区 WDK DirectX 9.0
- D3DFORMAT_OP_ZSTENCIL_WITH_ARBITRARY_COLOR_DEPTH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4924724a84da6506aa7cd08bbbd4abb2148e18b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567203"
---
# <a name="promoting-z-buffers-to-32-bits-per-pixel"></a>按像素将 Z 缓冲区升级到 32 位


## <span id="ddk_promoting_z_buffers_to_32_bits_per_pixel_gg"></span><span id="DDK_PROMOTING_Z_BUFFERS_TO_32_BITS_PER_PIXEL_GG"></span>


**本主题适用于 DirectX 8.0 及更高版本。**

显示驱动程序的显示设备不支持呈现到 z 和颜色不同的像素深度缓冲区必须以透明方式将 16 位 / 像素 (bpp) z 缓冲区到 32 bpp 提升以便在同一时间呈现 z 缓冲区和 32 bpp 颜色缓冲区。 但请注意，z 缓冲区不能同时具有模具位。 因此，应用程序不需要更正缓冲区像素的深度中这种不匹配。

如果驱动程序的显示设备可以呈现到 z 和颜色的不同像素深度的缓冲区，驱动程序设置 D3DFORMAT\_OP\_ZSTENCIL\_WITH\_任意\_颜色\_深度标志在中**dwOperations**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274) z 缓冲区格式的结构。 然后，Direct3D 运行时能让应用程序呈现到 z 和颜色像素深度的任何不匹配。

如果该驱动程序不会设置 D3DFORMAT\_OP\_ZSTENCIL\_WITH\_任意\_颜色\_z 缓冲区格式的深度，则运行时仅允许应用程序呈现到 32 bpp 的不匹配中的介绍性段落所述的颜色缓冲区和 16 bpp z 缓冲区与任何模具位。 在这种情况下，该驱动程序分配请求的 16 bpp z 缓冲区代替一个 32 bpp z 缓冲区。

如果 D3DFORMAT\_OP\_ZSTENCIL\_WITH\_任意\_颜色\_深度未设置，运行时不允许应用程序呈现到以下不匹配情况：

-   16 bpp 颜色缓冲区，同时在 32 bpp z 缓冲区。 用于呈现成功在此方案中，该驱动程序将需要替换 32 bpp z 缓冲区，将会降低 z 精度，会造成明显的项目的 16 bpp z 缓冲区。

-   其深度模具不占用相同数量的每像素位数为颜色缓冲区 （即，不匹配 z 和模具面） 的任何 z 格式。 若要成功执行在此方案中的呈现，驱动程序将必须更改的模具位数，还会导致明显的项目。

 

 





