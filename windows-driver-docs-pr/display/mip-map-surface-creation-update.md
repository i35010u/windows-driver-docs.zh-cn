---
title: MIP 贴图图面创建更新
description: MIP 贴图图面创建更新
ms.assetid: a89a11ed-d450-43bb-b0cd-75132d19dbc3
keywords:
- MIP 映射可呈现 WDK Direct3D
- D3DRENDERSTATE_MIPMAPLODBIAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f218561192944990233f59d9a6c7a6143adc2f9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379877"
---
# <a name="mip-map-surface-creation-update"></a>MIP 贴图图面创建更新


## <span id="ddk_mip_map_surface_creation_update_gg"></span><span id="DDK_MIP_MAP_SURFACE_CREATION_UPDATE_GG"></span>


在 DirectX 7.0 之前的附件 MIP 映射链通常包括仅 MIP 映射的子级别。 使用三次方环境映射的问世，这不再是这种情况。 三次方环境的每张人脸本身可能就是 MIP 映射，并且在这种情况下，形成一个三次方环境映射的人脸的表面的附件链可以组成多维数据集映射的其他人脸的链接，以及指向 MIP 映射的子级别。

MIP 映射图面上的附件链现在可包含指向不只是较低级别 MIP 映射图面，如少量新功能已引入 DDSCAPS2\_MIPMAPSUBLEVEL (请参阅[ **DDSCAPS2**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))此对话框和以下标志的结构)。 对于所有 MIP 映射链的顶级面都设置此位。 因此，给定 MIP 映射链可以找到通过遍历寻找 DDSCAPS2 的曲面图面的顶级附件列表来表示 MIP 映射链的下一最低级别的图面在顶级面\_MIPMAPSUBLEVEL功能位集。

若要确定图面是否显示三次方环境映射，在图面中查找的人脸功能位 DDSCAPS2\_立方体贴图。 如果 DDSCAPS\_MIPMAP 功能位未设置，此图面的附件列表包括的其他人脸的多维数据集映射正在创建的 (检查功能位 DDSCAPS2\_立方体贴图\_POSITIVEX、 DDSCAPS2\_立方体贴图\_NEGATIVEX、 DDSCAPS2\_立方体贴图\_POSITIVEY、 DDSCAPS2\_立方体贴图\_NEGATIVEY、 DDSCAPS2\_立方体贴图\_POSITIVEZ，DDSCAPS2\_立方体贴图\_NEGATIVEZ)。

如果 DDSCAPS\_设置 MIPMAP 功能位，则多维数据集映射图面上的附加图面上列表包含指向为立方体贴图与上面的其他人脸和下一级别的此人脸的 MIP 映射的链接。 可以通过 DDSCAPS2 标识 MIP 映射的子级\_MIPMAPSUBLEVEL 位上面所述。

### <a name="span-idd3drenderstatemipmaplodbiasspanspan-idd3drenderstatemipmaplodbiasspand3drenderstatemipmaplodbias"></a><span id="d3drenderstate_mipmaplodbias"></span><span id="D3DRENDERSTATE_MIPMAPLODBIAS"></span>D3DRENDERSTATE\_MIPMAPLODBIAS

尽管此呈现器状态是已过时，但其功能已被移到纹理阶段状态，也就是说，D3DRENDERSTATE\_MIPMAPLODBIAS 是完全相当于 D3DTSS\_MIPMAPLODBIAS 中的枚举器D3DTEXTURESTAGESTATETYPE 为纹理阶段零的枚举类型。 在接收 D3DRENDERSTATE\_MIPMAPLODBIAS 呈现通过旧界面的状态，您的驱动程序应只需将其映射到相同的代码处理 D3DTSS\_纹理 MIPMAPLODBIAS 暂存零。

MIP 映射 LOD 偏差是用来更改级别细节 (LOD) 偏差的浮点值。 此值偏移量计算的三线性纹理 MIP 映射级别的值。 它通常是范围介于-1.0 到 1.0;默认值为 0.0。 当前 WHQL/DCT 测试需要 MIP 映射 LOD 偏置的范围为 3.0-3.0 中运行。

（+ /-1.0) 每个单元偏差偏差值恰好一个 MIP 映射级别由所选内容。 负偏差会导致使用更大 MIP 贴图级别，从而导致锐利但多个别名映像。 正偏差会导致使用较小的 MIP 贴图级别，从而导致模糊的图像。 此外将应用负偏差会导致较小的纹理数据，这些可提高某些系统上的性能数据量的引用。

**请注意**   DirectX 9.0 和更高版本的应用程序可以使用 D3DSAMP\_MIPMAPLODBIAS D3DSAMPLERSTATETYPE 枚举来控制 mipmap 的详细信息偏差级别中的值。 在运行时映射用户模式下采样器状态 (D3DSAMP\_*Xxx*) 到内核模式 D3DTSS\_*Xxx*值，因此驱动程序不需要处理用户模式下采样器状态。 驱动程序仍应处理 D3DTSS\_MIPMAPLODBIAS 值。 有关 D3DSAMPLERSTATETYPE 详细信息，请参阅最新的 DirectX SDK 文档。

 

 

 





