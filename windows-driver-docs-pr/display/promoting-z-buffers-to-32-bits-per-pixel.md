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
ms.openlocfilehash: 92fa6f3caa721b4cf166f4393a4fdc1ed94ac69e
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064652"
---
# <a name="promoting-z-buffers-to-32-bits-per-pixel"></a>按像素将 Z 缓冲区升级到 32 位


## <span id="ddk_promoting_z_buffers_to_32_bits_per_pixel_gg"></span><span id="DDK_PROMOTING_Z_BUFFERS_TO_32_BITS_PER_PIXEL_GG"></span>


**本主题适用于 DirectX 8.0 和更高版本。**

显示设备不支持对具有不同像素深度的 z 和颜色缓冲区进行呈现的显示驱动程序必须以透明方式将16位/像素提升 (bpp) z 缓冲区到 32 bpp，以便同时呈现 z 缓冲区和 32 bpp 颜色缓冲区。 但请注意，z 缓冲区还不能有模具位。 因此，应用程序不需要更正缓冲区像素深度中的此不匹配。

如果驱动程序的显示设备可以呈现为 z 和颜色缓冲区的不同像素深度，则驱动程序会 \_ \_ \_ \_ \_ \_ 在 z 缓冲区格式的[**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwOperations**成员中，将 D3DFORMAT OP ZSTENCIL 设置为任意颜色深度标志。 然后，Direct3D 运行时让应用程序呈现为 z 和颜色像素深度的任意不匹配。

如果驱动程序未将 D3DFORMAT \_ OP \_ ZSTENCIL 设置 \_ \_ \_ \_ 为适用于 z 缓冲区格式的任意颜色深度，则运行时只允许应用程序呈现 32 bpp 颜色缓冲区与 16 bpp z 缓冲区的不匹配，其中不包含简介段中所述的模具位。 在这种情况下，驱动程序会分配 32 bpp z 缓冲区来替代请求的 16 bpp z 缓冲区。

如果 \_ \_ 未设置 D3DFORMAT OP ZSTENCIL \_ 和 \_ 任意 \_ 颜色 \_ 深度，则运行时不会使应用程序呈现为以下不匹配方案：

-   16 bpp 彩色缓冲区和 32 bpp z 缓冲区。 若要在这种情况下呈现成功，驱动程序必须将 16 bpp z 缓冲区替换为 32 bpp z 缓冲区，这会降低 z 精度并导致明显的项目。

-   任何 z 格式，其深度模具与颜色缓冲区的每个像素的位数不相同 (换言之，不匹配的 z 和模具图面) 。 若要在这种情况下呈现成功，驱动程序必须更改模具位的数目，这也会导致明显的项目。

 

