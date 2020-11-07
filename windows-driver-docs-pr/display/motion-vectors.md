---
title: 动作矢量
description: 动作矢量
ms.assetid: 463a2434-7f3e-4960-a595-8ca2ccc21504
keywords:
- macroblocks WDK DirectX VA，运动向量
- 运动向量 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1dc47012631e129aecbfeaa1adfb820c8925e220
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361569"
---
# <a name="motion-vectors"></a>动作矢量


## <span id="ddk_motion_vectors_gly"></span><span id="DDK_MOTION_VECTORS_GLY"></span>


如果图片不是图片内部 ( [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicIntra** 成员为零) ，则运动向量包含在宏块控件命令结构中。 结构中包含的运动矢量的数目取决于图片的类型 (例如， *B picture* 或 *P picture* ) 。 此外，如果宏块中所定义 (基于的参考图片选择，则在使用) 中，每个运动矢量的参考图片选择索引也包含在宏块控制-命令结构中。

为每个宏块控件命令结构中的运动矢量保留的空间通常是四个运动向量所需的数量。 每个运动向量都是使用 [**DXVA \_ MVvalue**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mvvalue) 结构指定的。 通常情况下，这两种情况下会包括这两个 nonintra。 不 (在 *dxva* 头文件中显式定义的其余情况) 如下所示：

-   如果正在 (使用 *OBMC* ，则 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicOBMC** 成员为 1) 并且图片不是 PB 图片的 B 部分 (此结构的 **bPicBinPB** 成员为零) ，10个运动向量的空间以及与16字节边界对齐所需的任何额外空间都将包括在内。

-   如果正在 (使用 OBMC，则 DXVA PictureParameters 结构的 **bPicOBMC** 成员 \_ 是 1) ，图片是 PB 图片的 B 部分 (此结构的 **bPicBinPB** 成员为 1) ，11个运动向量的空间加上与16字节边界对齐所需的任何附加空间）都包含在内。

-   如果 OBMC 未被使用 (则 DXVA PictureParameters 结构的 **bPicOBMC** 成员 \_ 为零) ，图片是 PB 图片的 B 的一部分 (此结构的 **bPicBinPB** 成员为 1) ，并且每个宏块的 bPic4Mvallowed 成员都允许使用四个运动向量 (此结构的 **bPic4Mvallowed** 成员为 1) ，五个运动向量的空间加上与16字节边界对齐所需的任何附加空间，均包括在内。

