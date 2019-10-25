---
title: 按像素将 Z 缓冲区升级到 32 位
description: 按像素将 Z 缓冲区升级到 32 位
ms.assetid: 6b7dddab-e154-44e8-a4e3-45bd706ed638
keywords:
- z 缓冲 WDK DirectX 9。0
- 颜色缓冲区 WDK DirectX 9。0
- D3DFORMAT_OP_ZSTENCIL_WITH_ARBITRARY_COLOR_DEPTH
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 858a99bea97c0168a7ca104112cc93ab99dbcbd0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72826037"
---
# <a name="promoting-z-buffers-to-32-bits-per-pixel"></a>按像素将 Z 缓冲区升级到 32 位


## <span id="ddk_promoting_z_buffers_to_32_bits_per_pixel_gg"></span><span id="DDK_PROMOTING_Z_BUFFERS_TO_32_BITS_PER_PIXEL_GG"></span>


**本主题适用于 DirectX 8.0 和更高版本。**

显示设备不支持对具有不同像素深度的 z 和颜色缓冲区进行呈现的显示驱动程序必须以透明方式将16位每像素（bpp） z 缓冲区提升为 32 bpp，以便同时呈现 z 缓冲区和 32 bpp 颜色缓冲区。 但请注意，z 缓冲区还不能有模具位。 因此，应用程序不需要更正缓冲区像素深度中的此不匹配。

如果驱动程序的显示设备可以呈现为 z 和颜色缓冲区的不同像素深度，则驱动程序将设置 D3DFORMAT\_OP\_ZSTENCIL\_，并\_中的**dwOperations**成员\_z 缓冲区格式的[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构。 然后，Direct3D 运行时让应用程序呈现为 z 和颜色像素深度的任意不匹配。

如果驱动程序未将 D3DFORMAT 设置为\_\_ZSTENCIL\_\_任意\_色\_z 缓冲器格式，则运行时只会使应用程序呈现为 32 bpp 颜色缓冲区和 16 bpp z 缓冲区不匹配模具位，如简介段中所述。 在这种情况下，驱动程序会分配 32 bpp z 缓冲区来替代请求的 16 bpp z 缓冲区。

如果未设置 D3DFORMAT\_OP\_ZSTENCIL\_\_任意\_色\_深度，则运行时不会使应用程序呈现为以下不匹配方案：

-   16 bpp 彩色缓冲区和 32 bpp z 缓冲区。 若要在这种情况下呈现成功，驱动程序必须将 16 bpp z 缓冲区替换为 32 bpp z 缓冲区，这会降低 z 精度并导致明显的项目。

-   任何 z 格式，其深度模具的每个像素的位数均不等于颜色缓冲区（换言之，z 和模具表面不匹配）。 若要在这种情况下呈现成功，驱动程序必须更改模具位的数目，这也会导致明显的项目。

 

 





