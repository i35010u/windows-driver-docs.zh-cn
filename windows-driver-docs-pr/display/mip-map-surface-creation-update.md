---
title: MIP 贴图图面创建更新
description: MIP 贴图图面创建更新
keywords:
- MIP 地图面 WDK Direct3D
- D3DRENDERSTATE_MIPMAPLODBIAS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a673a5754ed5b10830ea43a6c76d4fbe23f03fd3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838073"
---
# <a name="mip-map-surface-creation-update"></a>MIP 贴图图面创建更新


## <span id="ddk_mip_map_surface_creation_update_gg"></span><span id="DDK_MIP_MAP_SURFACE_CREATION_UPDATE_GG"></span>


在 DirectX 7.0 之前，MIP map 的附件链通常仅包括该 MIP 地图的子级别。 随着三个三个环境映射的出现，这种情况并不是如此。 每个平面环境的每个面本身都可以是一个 MIP 图，因此，形成一个平面环境地图表面的图面的附件链可以包含指向多维数据集映射的其他面的链接，还可以包含指向 MIP 地图子层的链接。

由于 MIP 贴图图面的附件链现在可以包含指向除更低级别 MIP 地图之外的表面的链接，所以引入了新的功能位，DDSCAPS2 \_ MIPMAPSUBLEVEL (查看此的 [**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85)) 结构，并) 以下标志。 此位是为 MIP 地图链的所有顶级曲面设置的。 因此，在给定 MIP 地图链的顶级图面上，您可以通过遍历顶级曲面的附件列表（查找具有 DDSCAPS2 \_ MIPMAPSUBLEVEL 功能位集的图面）来查找表示 mip 地图链下一最低级别的图面。

若要确定图面是否为立方米环境图的正面，请检查 surface DDSCAPS2 \_ 立方体贴图。 如果 \_ 未设置 DDSCAPS MIPMAP 功能位，此图面的附件列表将包含正在创建的多维数据集映射的其他面， (检查功能位 DDSCAPS2 \_ 立方体贴图 \_ POSITIVEX、DDSCAPS2 \_ 立方体贴图 \_ NEGATIVEX、DDSCAPS2 \_ 立方体贴图 \_ POSITIVEY、DDSCAPS2 \_ 立方体贴图 \_ NEGATIVEY、DDSCAPS2 \_ 立方体贴图 \_ POSITIVEZ、DDSCAPS2 \_ 立方体贴图 \_ NEGATIVEZ) 。

如果设置了 DDSCAPS \_ MIPMAP 功能位，则多维数据集映射图面的附加 surface 列表将包含与上面相同的多维数据集映射的其他面的链接，还包含此人脸的下一个 MIP 地图级别。 可以通过上述 DDSCAPS2 MIPMAPSUBLEVEL 位标识 MIP map 的子层次 \_ 。

### <a name="span-idd3drenderstate_mipmaplodbiasspanspan-idd3drenderstate_mipmaplodbiasspand3drenderstate_mipmaplodbias"></a><span id="d3drenderstate_mipmaplodbias"></span><span id="D3DRENDERSTATE_MIPMAPLODBIAS"></span>D3DRENDERSTATE \_ MIPMAPLODBIAS

尽管此呈现状态已过时，但其功能已移动到纹理阶段状态，也就是说，D3DRENDERSTATE MIPMAPLODBIAS 与 \_ D3DTSS MIPMAPLODBIAS 枚举器完全等效于 \_ 纹理阶段0的 D3DTEXTURESTAGESTATETYPE 枚举类型。 在 \_ 通过旧接口接收 D3DRENDERSTATE MIPMAPLODBIAS render 状态时，驱动程序只需将其映射到为纹理阶段零处理 D3DTSS MIPMAPLODBIAS 的相同代码 \_ 。

MIP map LOD 偏量是一个浮点值，它用于更改) 偏差 (的详细级别。 此值偏移由 trilinear 纹理计算的 MIP map 级别的值。 它通常在-1.0 到1.0 的范围内;默认值为0.0。 当前的 WHQL/DCT 测试要求 MIP map LOD 偏量在-3.0 到3.0 的范围内操作。

每个单位偏差 (+/-1.0) 只偏移一个 MIP map 级别的选定内容。 负偏差会导致使用较大的 MIP 地图级别，导致图像更清晰但图像更清晰。 正偏差导致使用较小的 MIP 贴图级别，从而导致 blurrier 图像。 应用负偏差还会导致引用较小的纹理数据量，这可以提高某些系统的性能。

**注意**   DirectX 9.0 和更高版本的应用程序可使用 \_ D3DSAMPLERSTATETYPE 枚举中的 D3DSAMP MIPMAPLODBIAS 值控制 mipmap 的详细信息偏移级别。 运行时将用户模式采样器状态映射 (D3DSAMP \_ *Xxx*) 为内核模式 D3DTSS \_ *Xxx* 值，以便驱动程序无需处理用户模式采样器状态。 驱动程序仍应处理 D3DTSS \_ MIPMAPLODBIAS 值。 有关 D3DSAMPLERSTATETYPE 的详细信息，请参阅最新的 DirectX SDK 文档。

 

 

