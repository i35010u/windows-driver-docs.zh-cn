---
title: 动作矢量
description: 动作矢量
ms.assetid: 463a2434-7f3e-4960-a595-8ca2ccc21504
keywords:
- 宏块 WDK DirectX VA，动作矢量
- 动作矢量 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1692ceb4dff47464663f1ba8ae251c51a4e17ae4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566548"
---
# <a name="motion-vectors"></a>动作矢量


## <span id="ddk_motion_vectors_gly"></span><span id="DDK_MOTION_VECTORS_GLY"></span>


如果图片不是内部图片 ( **bPicIntra**的成员**DXVA\_PictureParameters**或*P 图片*)。 此外，如果基于宏块的引用的图片所选内容 （如 H.263 Annex U 中定义） 正在使用中，然后每个运动向量的引用图片选择索引还包括宏块控制命令结构中。

为每个宏块控制命令结构中的动作矢量保留的空间通常是所需的四个动作矢量的量。 使用指定每个动作矢量[ **DXVA\_MVvalue** ](https://msdn.microsoft.com/library/windows/hardware/ff564004)结构。 这些常见的情况下包括两个上述 nonintra 情况。 剩余的情况下 (在中未显式定义*dxva.h*标头文件) 如下所示：

-   如果*OBMC*正在使用中 ( **bPicOBMC**的成员[ **DXVA\_PictureParameters** ](https://msdn.microsoft.com/library/windows/hardware/ff564012)结构为 1) 和图片不 PB 图片的 B 部分 ( **bPicBinPB**此结构的成员为零)，为 10 个动作矢量，加上任何额外的空间为 16 字节边界对齐所需的空间，则包含。

-   如果 OBMC 正在使用中 ( **bPicOBMC** DXVA 成员\_PictureParameters 结构为 1) 和图片是 PB 图片的 B 部分 ( **bPicBinPB**此结构的成员为 1)，为 11 的空间包含动作矢量，加上对齐到 16 字节边界，所需任何额外的空间。

-   如果未使用 OBMC ( **bPicOBMC** DXVA 成员\_PictureParameters 结构为零)，图片是 PB 图片的 B 部分 ( **bPicBinPB**此结构的成员为 1)，和四个允许每个宏块的运动向量 ( **bPic4Mvallowed**此结构的成员为 1)，则包含五个动作矢量，加上任何额外的空间对齐到 16 字节边界，所需的空间。

 

 





