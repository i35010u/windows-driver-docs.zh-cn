---
title: 动作矢量
description: 动作矢量
ms.assetid: 463a2434-7f3e-4960-a595-8ca2ccc21504
keywords:
- macroblocks WDK DirectX VA，运动向量
- 运动向量 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ce9084609df3adadf74508d6c9b64cb2c3c34ee
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840553"
---
# <a name="motion-vectors"></a>动作矢量


## <span id="ddk_motion_vectors_gly"></span><span id="DDK_MOTION_VECTORS_GLY"></span>


如果图片不是图片内部（ **DXVA\_** 的**bPicIntra**成员，则为 "PictureParameters" 或 " *P" 图*）。 此外，如果正在使用基于宏块的参考图片选择（如在中定义的），则每个运动矢量的参考图片选择索引也包含在宏块控制-命令结构中。

为每个宏块控件命令结构中的运动矢量保留的空间通常是四个运动向量所需的数量。 每个运动向量都使用[**DXVA\_MVvalue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mvvalue)结构来指定。 通常情况下，这两种情况下会包括这两个 nonintra。 其余情况（未在*dxva*头文件中显式定义）如下所示：

-   如果正在使用*OBMC* （ [ **\_DXVA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)的**bPicOBMC**成员为1），而图片不是 PB 图片的 B 部分（此结构的**bPicBinPB**成员为零），空间表示10个运动向量，加上包括与16字节边界对齐所需的任何额外空间。

-   如果正在使用 OBMC （\_DXVA 的**bPicOBMC**成员为1），并且图片是 PB 图片的 B 部分（此结构的**bPicBinPB**成员为1）、包含11个运动向量的空间以及所需的任何额外空间包含与16字节边界对齐。

-   如果未使用 OBMC （DXVA\_PictureParameters 结构的**bPicOBMC**成员为零），则图片是 PB 图片的 B 部分（此结构的**bPicBinPB**成员为1），并且允许每个宏块使用四个运动向量（此结构的**bPic4Mvallowed**成员为1），包含五个运动向量的空间以及与16字节边界对齐所需的任何额外空间。

 

 





