---
title: 创建压缩纹理图面
description: 创建压缩纹理图面
ms.assetid: 6d1cc079-642c-4662-ae72-c0362d8a5b2a
keywords:
- 绘制压缩纹理 WDK DirectDraw，创建
- DirectDraw 压缩纹理 WDK Windows 2000 显示，创建
- 压缩的纹理面 WDK DirectDraw，创建
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84e3dba3c4d60583bdae6c035f8ffd6c12b6329d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839023"
---
# <a name="creating-the-compressed-texture-surface"></a>创建压缩纹理图面


## <span id="ddk_creating_the_compressed_texture_surface_gg"></span><span id="DDK_CREATING_THE_COMPRESSED_TEXTURE_SURFACE_GG"></span>


每当 DirectDraw 请求驱动程序创建图面时，驱动程序必须确定是否需要创建一个压缩的纹理图面。 若要确定这一点，驱动程序必须在[**DDSURFACEDESC2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构中检查以前已为所创建的图面设置的信息。 你的驱动程序必须包含以下验证步骤（与任何图面一样）：

-   检查[**DDSCAPS**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构的**dwFlags**成员中的 DDSCAPS\_纹理标志。

-   检查正在创建的图面[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwFlags**成员中的 DDPF\_FOURCC 标志。 在以下**dwFourCC**检查之前应进行此检查。

-   在要创建的图面上检查[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwFourCC**成员中是否有一个 DXT 代码。

-   检查[**DDSURFACEDESC2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550340(v=vs.85))结构的宽度和高度成员（**dwWidth**和**dwHeight**）。 DirectDraw 将这些成员设置为4像素的倍数。

 

 





