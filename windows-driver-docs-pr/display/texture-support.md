---
title: 纹理支持
description: 纹理支持
ms.assetid: 8ae4d4bf-9fef-4e5e-a88a-5cb93519c802
keywords:
- 绘图页上翻转 WDK DirectDraw，纹理
- DirectDraw 翻转 WDK Windows 2000 显示，纹理
- 页翻转 WDK DirectDraw，纹理
- 翻转 WDK DirectDraw，纹理
- 纹理 WDK DirectDraw 翻转
- 三维表面之上翻转 WDK DirectDraw
- 显示 WDK DirectDraw 翻转
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e03513d780c4ccdbcf70b84919c46266c84f7672
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545794"
---
# <a name="texture-support"></a>纹理支持


## <span id="ddk_texture_support_gg"></span><span id="DDK_TEXTURE_SUPPORT_GG"></span>


在 3D 空间中的纹理翻转像任何其他面一样。 一个*纹理*是只是一个平面映像，具有到三维表面之上的位设置为指定可以将转换 （纹理映射）。 纹理可以映射到三维表面之上，动作可以顺利地呈现的页面翻转纹理。 翻转等待呈现器完成读取 （如正在等待扫描行）。 如果翻转的驱动程序支持纹理，它必须能够识别并进行相应处理。 纹理的更多详细信息，请参阅[Direct3D 纹理管理](direct3d-texture-management.md)。

 

 





