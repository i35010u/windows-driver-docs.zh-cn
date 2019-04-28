---
title: 将图面设为 FOURCC 格式
description: 将图面设为 FOURCC 格式
ms.assetid: 947b73c9-3f1d-485e-9966-815b40a06342
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示纹理格式的属性列
- 纹理格式列出了 WDK DirectX 8.0
- DPIXELFORMAT
- 图面格式 WDK DirectX 8.0
- Fourcc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c25c9a13bcb7b2c48f75320b5b39f047f528b3fa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350053"
---
# <a name="surface-formats-as-fourccs"></a>将图面设为 FOURCC 格式


## <span id="ddk_surface_formats_as_fourccs_gg"></span><span id="DDK_SURFACE_FORMATS_AS_FOURCCS_GG"></span>


三个新的图面上格式定义的 DirectX 8.0，D3DFMT\_Q8W8V8U8、 D3DFMT\_V16U16 和 D3DFMT\_W11V11U10，传递给驱动程序，因为*Fourcc*。 这意味着各个位深度和掩码字段[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)未初始化数据结构和它们的值是未定义。 因此，处理这些三种格式的驱动程序必须不依赖于位计数或掩码中像素格式，但必须根据需要这些计算。 例如，在计算的面音调其中一种类型**dwRGBBitCount**的像素格式的字段不能使用。 所有其他格式而不 YUV、 DXT 和 IHV 特定的扩展格式映射到的旧 DDPIXELFORMAT 表示形式传递给驱动程序时，因此，有效像素格式和蒙板中的像素格式的数据结构。

 

 





