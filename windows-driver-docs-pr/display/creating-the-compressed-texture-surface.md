---
title: 创建压缩的纹理图面
description: 创建压缩的纹理图面
ms.assetid: 6d1cc079-642c-4662-ae72-c0362d8a5b2a
keywords:
- 绘制压缩的纹理 WDK DirectDraw 创建
- DirectDraw 压缩的纹理 WDK Windows 2000 显示，请创建
- 压缩的纹理的图面 WDK DirectDraw 创建
- WDK DirectDraw，压缩的纹理的图面
- 纹理 WDK DirectDraw 压缩
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d81b763acf3677e1062855602c7ff9d9584ff60
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526714"
---
# <a name="creating-the-compressed-texture-surface"></a>创建压缩的纹理图面


## <span id="ddk_creating_the_compressed_texture_surface_gg"></span><span id="DDK_CREATING_THE_COMPRESSED_TEXTURE_SURFACE_GG"></span>


每当 DirectDraw 请求驱动程序创建图面，该驱动程序必须确定是否正在要求它创建压缩的纹理图面。 若要确定这一点，该驱动程序必须检查以前的 DirectDraw 中设置的信息[ **DDSURFACEDESC2** ](https://msdn.microsoft.com/library/windows/hardware/ff550340)面的正在创建的结构。 您的驱动程序必须 （使用任何图面） 包括以下验证步骤：

-   检查 DDSCAPS\_中的纹理标志**dwFlags**的成员[ **DDSCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff550286)结构。

-   检查 DDPF\_FOURCC 标志**dwFlags**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)面的正在创建的结构。 在以下前应进行此检查**dwFourCC**检查。

-   检查在 DXT 代码之一**dwFourCC**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)面的正在创建的结构。

-   检查的宽度和高度的成员 (**dwWidth**并**dwHeight**) 的[ **DDSURFACEDESC2** ](https://msdn.microsoft.com/library/windows/hardware/ff550340)结构。 DirectDraw 将这些成员设置为 4 个像素的倍数。

 

 





