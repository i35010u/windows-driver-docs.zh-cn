---
title: 动态纹理
description: 动态纹理
ms.assetid: 5e96b33c-a07c-4f58-a016-14d8d925285e
keywords:
- 纹理 WDK DirectX 9.0
- 动态纹理 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d6d55b2c82adb147ed1e6d9a03f449615874565
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576722"
---
# <a name="dynamic-textures"></a>动态纹理


## <span id="ddk_dynamic_textures_gg"></span><span id="DDK_DYNAMIC_TEXTURES_GG"></span>


动态纹理是几乎完全相同[动态缓冲区](dynamic-vertex-and-index-buffers.md)。 因为应用程序也经常锁定和修改动态纹理，驱动程序应：

-   优化纹理上传或平铺速度。

-   如果硬件体系结构允许驱动程序使用 nontiled 纹理 nontiled 的方式创建动态纹理。 这是因为如果不要求驱动程序以撤消动态纹理平铺纹理处于锁定状态时接收到的性能改进已超出从平铺的填充率优势。

-   类似于中的说明设置了多个缓冲[动态顶点和索引缓冲区](dynamic-vertex-and-index-buffers.md)。 也就是说，设置 DDLOCK\_OKTOSWAP 位锁定动态纹理。 同样，在本地的视频内存中存储动态纹理也会导致系统性能会受到影响，如果应用程序写入此类纹理以无序的方式。 因此，应将该驱动程序存储中的动态纹理[AGP](agp-support.md)内存。

 

 





