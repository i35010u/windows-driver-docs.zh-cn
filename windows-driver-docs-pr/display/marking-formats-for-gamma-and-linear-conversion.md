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
ms.openlocfilehash: 8d77fd3ff8003466cfaf8165b07694e14c305953
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840575"
---
# <a name="marking-formats-for-gamma-and-linear-conversion"></a>标记灰度和线性转换的格式


## <span id="ddk_marking_formats_for_gamma_and_linear_conversion_gg"></span><span id="DDK_MARKING_FORMATS_FOR_GAMMA_AND_LINEAR_CONVERSION_GG"></span>


DirectX 9.0 版本驱动程序标记线性或伽玛转换的纹理格式，以便它能够确定是否转换这些格式的纹理以便准确地处理或渲染它们。

纹理内容通常以 sRGB 格式存储，并以伽玛格式进行更正。 但是，若要使像素管道对 sRGB 格式的纹理执行准确的混合操作，驱动程序必须先将这些纹理转换为线性格式，然后再从中进行读取。 当像素管道准备好将这些纹理写入渲染器目标时，驱动程序必须将这些纹理转换回 sRGB 格式。 通过这种方式，像素管道在线性空间中执行所有操作。

驱动程序在[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwOperations**成员中指定下列标志，以使纹理图面的格式标记转换格式：

-   D3DFORMAT\_OP\_SRGBREAD，以指示纹理是否已更正伽玛2.2 （sRGB 或 not），以及是否必须通过驱动程序将其转换为线性格式以用于混合操作或用于查找时的采样器。

-   D3DFORMAT\_OP\_SRGBWRITE，指示在写出到呈现器目标时，像素管道是否应正确地纠正为 sRGB 空间。

 

 





