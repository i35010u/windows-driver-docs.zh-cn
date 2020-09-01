---
title: 标记灰度和线性转换的格式
description: 标记灰度和线性转换的格式
ms.assetid: 1285b04e-b67a-46d2-82b2-3cde433bf578
keywords:
- 伽玛更正 WDK DirectX 9.0，标记伽玛转换的格式
- 标记转换的格式 WDK DirectX 9。0
- 线性转换 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f04f63ab3750437f07d1f21c23ad6dbbf786cfa2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064742"
---
# <a name="marking-formats-for-gamma-and-linear-conversion"></a>标记灰度和线性转换的格式


## <span id="ddk_marking_formats_for_gamma_and_linear_conversion_gg"></span><span id="DDK_MARKING_FORMATS_FOR_GAMMA_AND_LINEAR_CONVERSION_GG"></span>


DirectX 9.0 版本驱动程序标记线性或伽玛转换的纹理格式，以便它能够确定是否转换这些格式的纹理以便准确地处理或渲染它们。

纹理内容通常以 sRGB 格式存储，并以伽玛格式进行更正。 但是，若要使像素管道对 sRGB 格式的纹理执行准确的混合操作，驱动程序必须先将这些纹理转换为线性格式，然后再从中进行读取。 当像素管道准备好将这些纹理写入渲染器目标时，驱动程序必须将这些纹理转换回 sRGB 格式。 通过这种方式，像素管道在线性空间中执行所有操作。

驱动程序在[**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwOperations**成员中指定下列标志，以使纹理图面的格式标记转换格式：

-   D3DFORMAT \_ OP \_ SRGBREAD，用于指示纹理是否已更正伽玛 2.2 (sRGB 或不) ，以及在查找时，是否必须由驱动程序将其转换为线性格式（用于混合操作或采样器）。

-   D3DFORMAT \_ OP \_ SRGBWRITE，用于指示在写出到呈现器目标时，像素管道是否应伽玛正确地转换回 sRGB 空间。

 

