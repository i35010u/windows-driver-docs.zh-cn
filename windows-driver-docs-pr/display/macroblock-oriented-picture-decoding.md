---
title: 面向宏块的图片解码
description: 面向宏块的图片解码
keywords:
- macroblocks WDK DirectX VA
- 压缩的图片解码 WDK DirectX VA，面向宏块的图片解码
- 图片解码 WDK DirectX VA，已压缩
- macroblocks WDK DirectX VA，关于面向宏块的图片解码
- 视频解码 WDK DirectX VA，压缩图片
- 解码视频 WDK DirectX VA，压缩图片
- 视频解码 WDK DirectX VA，面向宏块的图片解码
- 解码视频 WDK DirectX VA，面向宏块的图片解码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bc79e884693ce95331d2304262a844e554fc889
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813801"
---
# <a name="macroblock-oriented-picture-decoding"></a>面向宏块的图片解码


## <span id="ddk_macroblock_oriented_picture_decoding_gg"></span><span id="DDK_MACROBLOCK_ORIENTED_PICTURE_DECODING_GG"></span>


宏块是视频解码过程的基本单位。 宏块由亮度 (Y) 样本和两个对应的色度数组 (Cb 和 Cr) 示例组成。 在已建立的视频编码标准中，macroblocks 在亮度样本维度中是16x16 块。 如果以4:2:0 格式编码视频，则两个色度数组的高度和宽度均为宏块的亮度数组的宽度的一半。 如果以4:2:2 格式编码视频，则两个色度数组的高度和宽度均为宏块的亮度数组的宽度。 如果以4:4:4 格式编码视频，则两个色度数组的大小与宏块的亮度数组大小相同。

可以使用具有一个或多个运动向量的运动补偿预测宏块，或者在没有此类预测的情况下将其编码为内部。 确定宏块是否预测后，剩余的信号优化（如果有）将以残差数据块的形式添加。 在已建立的视频编码标准中，这些残留差异数据块是8x8 的，因此需要四个残留差异数据块来涵盖16x16 亮度宏块。

 

 





