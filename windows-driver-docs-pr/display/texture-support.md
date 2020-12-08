---
title: 纹理支持
description: 纹理支持
keywords:
- 绘图页翻转 WDK DirectDraw，纹理
- DirectDraw 翻转 WDK Windows 2000 显示，纹理
- 页面翻转 WDK DirectDraw，纹理
- 翻转 WDK DirectDraw，纹理
- 纹理 WDK DirectDraw，翻转
- 3D surface 反向 WDK DirectDraw
- surface DirectDraw，翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51f9f241aa24c843a9c82a5ab0451e587608d6cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838933"
---
# <a name="texture-support"></a>纹理支持


## <span id="ddk_texture_support_gg"></span><span id="DDK_TEXTURE_SUPPORT_GG"></span>


三维空间中的纹理与任何其他表面的翻转方式相同。 *纹理* 只是一个平面图像，其位设置为指定可将其转换 (纹理映射) 到三维表面。 纹理可以映射到3D 图面上，可以通过页面翻转纹理来平滑地呈现运动。 反向等待呈现器完成读取 (如等待扫描行) 。 如果翻转驱动程序支持纹理，则它必须能够相应地识别和处理它们。 有关纹理的详细信息，请参阅 [Direct3D 纹理管理](direct3d-texture-management.md)。

 

 





