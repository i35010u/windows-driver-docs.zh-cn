---
title: 创建压缩纹理图面
description: 创建压缩纹理图面
keywords:
- 绘制压缩纹理 WDK DirectDraw，创建
- DirectDraw 压缩纹理 WDK Windows 2000 显示，创建
- 压缩的纹理面 WDK DirectDraw，创建
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e3ddf664d609688ad8a2e5d26adb1286a1ee3c92
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832797"
---
# <a name="creating-the-compressed-texture-surface"></a>创建压缩纹理图面


## <span id="ddk_creating_the_compressed_texture_surface_gg"></span><span id="DDK_CREATING_THE_COMPRESSED_TEXTURE_SURFACE_GG"></span>


每当 DirectDraw 请求驱动程序创建图面时，驱动程序必须确定是否需要创建一个压缩的纹理图面。 若要确定这一点，驱动程序必须在 [**DDSURFACEDESC2**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85)) 结构中检查以前已为所创建的图面设置的信息。 你的驱动程序必须包括以下验证步骤 (与任何图面) ：

-   \_在 [**DDSCAPS**](/previous-versions/windows/hardware/drivers/ff550286(v=vs.85))结构的 **DWFLAGS** 成员中检查 DDSCAPS 纹理标志。

-   检查 \_ 正在创建的图面 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的 **DWFLAGS** 成员中的 DDPF FOURCC 标志。 在以下 **dwFourCC** 检查之前应进行此检查。

-   在要创建的图面上检查 [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的 **dwFourCC** 成员中是否有一个 DXT 代码。

-   检查 "宽度" 和 "高度" 成员 (" [**DDSURFACEDESC2**](/previous-versions/windows/hardware/drivers/ff550340(v=vs.85)) " 结构的 " **dwWidth** " 和 " **dwHeight** ") 。 DirectDraw 将这些成员设置为4像素的倍数。

 

