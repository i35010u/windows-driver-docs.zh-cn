---
title: 标记灰度和线性转换的格式
description: 标记灰度和线性转换的格式
ms.assetid: 1285b04e-b67a-46d2-82b2-3cde433bf578
keywords:
- 灰度校正 WDK DirectX 9.0 中，将标记格式的 gamma 转换
- 将标记转换 WDK DirectX 9.0 的格式
- 线性转换 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5939fbadf9cb4ea6ff5ab5fb22ca4b0257dbff6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347524"
---
# <a name="marking-formats-for-gamma-and-linear-conversion"></a>标记灰度和线性转换的格式


## <span id="ddk_marking_formats_for_gamma_and_linear_conversion_gg"></span><span id="DDK_MARKING_FORMATS_FOR_GAMMA_AND_LINEAR_CONVERSION_GG"></span>


DirectX 9.0 版本驱动程序将为纹理格式标记线性或灰度转换以便它可以确定是否将转换这些格式，以准确地处理或呈现它们的纹理。

纹理的内容通常存储在 sRGB 格式，这是更正的 gamma。 但是，像素管道执行对 sRGB 格式纹理的准确混合操作，该驱动程序必须转换这些纹理的线性格式读取前从它们。 准备好这些纹理输出到呈现器目标像素管道时，该驱动程序必须将这些纹理转换回 sRGB 格式。 在这种方式，像素管道执行线性空间中的所有操作。

该驱动程序指定中的以下标志**dwOperations**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)纹理表面的格式来标记的格式的结构转换：

-   D3DFORMAT\_OP\_SRGBREAD 来指示纹理是 gamma 2.2 更正或不 (sRGB 或不)，并且它必须转换为线性格式由驱动程序用于混合操作或为采样器在查找时。

-   D3DFORMAT\_OP\_SRGBWRITE 以指示是否像素管道应正确 gamma 回 sRGB 空间写出到呈现器目标时。

 

 





