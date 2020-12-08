---
title: 动态纹理
description: 动态纹理
keywords:
- 纹理 WDK DirectX 9。0
- 动态纹理 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ac24e0130c3799b246efe63e0ec55c93483e0e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799693"
---
# <a name="dynamic-textures"></a>动态纹理


## <span id="ddk_dynamic_textures_gg"></span><span id="DDK_DYNAMIC_TEXTURES_GG"></span>


动态纹理几乎与 [动态缓冲区](dynamic-vertex-and-index-buffers.md)完全相同。 由于应用程序还经常锁定和修改动态纹理，因此驱动程序应：

-   优化纹理上传或平铺速度。

-   如果硬件体系结构允许驱动程序使用 nontiled 纹理，则以 nontiled 的方式创建动态纹理。 这是因为当纹理锁定时，从不要求驱动程序 untile 动态纹理的性能改进超出了平铺的填充率优势。

-   设置多个缓冲，类似于 [动态顶点和索引缓冲区](dynamic-vertex-and-index-buffers.md)中的说明。 也就是说，将 DDLOCK \_ OKTOSWAP 位设置为锁定动态纹理。 同样，如果应用程序以非顺序的方式写入到此类纹理，则在本地视频内存中存储动态纹理还会导致系统性能下降。 因此，驱动程序应将动态纹理存储在 [AGP](agp-support.md) 内存中。

 

 





