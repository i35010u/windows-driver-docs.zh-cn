---
title: 面向宏块的图片解码
description: 面向宏块的图片解码
ms.assetid: 7a416992-04d3-4307-83b3-9fb94c17d60e
keywords:
- 宏块 WDK DirectX VA
- 压缩的图片解码 WDK DirectX va，因此面向宏块的图片解码
- 图片解码 WDK DirectX VA，压缩
- 宏块 WDK DirectX va，因此有关面向宏块的图片解码
- 视频解码 WDK DirectX VA，压缩的图片
- 解码视频 WDK DirectX VA，压缩图片
- 视频解码 WDK DirectX VA，面向宏块的图片解码
- 解码视频 WDK DirectX va，因此面向宏块的图片解码
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c01270f84d0068459cfa792f20aa33ab3623c04
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380409"
---
# <a name="macroblock-oriented-picture-decoding"></a>面向宏块的图片解码


## <span id="ddk_macroblock_oriented_picture_decoding_gg"></span><span id="DDK_MACROBLOCK_ORIENTED_PICTURE_DECODING_GG"></span>


宏块是视频解码过程的基本单位。 宏块包括亮度 (Y) 示例的矩形数组和色度 （Cb 和 Cr） 示例的两个相应数组。 在已建立的视频编码标准，块效应是 16 x 16 亮度示例维度中的基块。 如果视频编码在 4:2:0 格式，则两个色度数组每个具有高度和宽度的宏块的亮度数组一半。 如果视频编码在 4:2:2 格式，两个色度数组，每个具有相同的高度和宏块的亮度数组的宽度的一半。 如果视频编码在 4:4:4 格式，则两个色度数组每个具有相同的大小与宏块的亮度数组。

宏块可能会使用一个或多个运动矢量运动补偿预测或可能编码为内部，而无需此类预测。 确定是否或不被预测宏块时，剩余的信号优化，如果有，添加后残留的差异数据块的形式。 在已建立的视频编码标准，这些残差差异数据块是 8 x 8，因此需要四个剩余的差异数据块以涵盖 16 x 16 亮度宏块。

 

 





