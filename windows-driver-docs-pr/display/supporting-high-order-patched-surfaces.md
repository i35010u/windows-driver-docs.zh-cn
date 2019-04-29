---
title: 支持高阶修补图面
description: 支持高阶修补图面
ms.assetid: 020fb91c-c8cd-43e8-a180-bbb2ef606be8
keywords:
- 高序位修补表面 WDK DirectX 9.0
- 位移映射 WDK DirectX 9.0
- 自适应分割呈现状态 WDK DirectX 9.0
- 分割映射 WDK DirectX 9.0
- 修补图面 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f1b8db2d23d05506d79ca214c079dd1a0f94689
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373409"
---
# <a name="supporting-high-order-patched-surfaces"></a>支持高阶修补图面


## <span id="ddk_supporting_high_order_patched_surfaces_gg"></span><span id="DDK_SUPPORTING_HIGH_ORDER_PATCHED_SURFACES_GG"></span>


DirectX 9.0 版驱动程序的设备的高序位修补图面必须指示此类功能位的支持，并能处理新的自适应分割支持自适应分割和偏移量映射呈现状态和位移映射纹理阶段状态。 有关自适应分割和偏移量映射的详细信息，请参阅最新版本的 DirectX SDK。

若要指示自适应分割和偏移量映射的支持，该驱动程序以下功能中的位设置**DevCaps2** D3DCAPS9 结构中的成员：

<span id="D3DDEVCAPS2_ADAPTIVETESSRTPATCH"></span><span id="d3ddevcaps2_adaptivetessrtpatch"></span>D3DDEVCAPS2\_ADAPTIVETESSRTPATCH  
设备可以自适应地对呈现器目标修补程序。

<span id="D3DDEVCAPS2_ADAPTIVETESSNPATCH"></span><span id="d3ddevcaps2_adaptivetessnpatch"></span>D3DDEVCAPS2\_ADAPTIVETESSNPATCH  
设备可以自适应地对 N 修补程序。

<span id="D3DDEVCAPS2_DMAPNPATCH"></span><span id="d3ddevcaps2_dmapnpatch"></span>D3DDEVCAPS2\_DMAPNPATCH  
设备 N 修补程序的支持位移映射。

<span id="D3DDEVCAPS2_PRESAMPLEDDMAPNPATCH"></span><span id="d3ddevcaps2_presampleddmapnpatch"></span>D3DDEVCAPS2\_PRESAMPLEDDMAPNPATCH  
设备 N 修补程序的支持 presampled 的位移映射。

若要指示 N 修补程序的细分显示设备可支持，驱动程序集的最大数目**MaxNpatchTessellationLevel**的最大数目 D3DCAPS9 结构中的成员。 为此最大数目的设备夹紧受到使用 presampled 的偏移量映射的应用程序。

该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

该驱动程序指定 D3DFORMAT\_OP\_DMAP 标志**dwOperations**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)为特定的结构要将标记为位移映射采样格式的图面上格式。 Direct3D 运行时创建纹理图面时，设置 DDSCAPS3\_DMAP 位**dwCaps3** DDSCAPSEX 的成员 ([**DDSCAPS2**](https://msdn.microsoft.com/library/windows/hardware/ff550292)) 结构若要指示可以进行纹理采样的分割单元中。

请注意，DirectX 9.0 和更高版本的驱动程序必须关闭 N 修补功能时，才 D3DRS 值\_PATCHSEGMENTS 呈现状态不小于 1.0 f。 DirectX 8.1 和更早的驱动程序不需要在这种方式中的行为。

以下自适应分割呈现状态以及它们的默认值是 DirectX 9.0 的新增功能：

D3DRS\_MAXTESSELLATIONLEVEL = 1.0 f

D3DRS\_MINTESSELLATIONLEVEL = 1.0 f

D3DRS\_ADAPTIVETESS\_X = 0.0f

D3DRS\_ADAPTIVETESS\_Y = 0.0f

D3DRS\_ADAPTIVETESS\_Z = 1.0f

D3DRS\_ADAPTIVETESS\_W = 0.0f

D3DRS\_ENABLEADAPTIVETESSELLATION = **FALSE**

D3DDMAPSAMPLER 采样器，也是 DirectX 9.0 的新增功能，用于在分割单元设置位移映射纹理。

**请注意**   DirectX 9.0 和更高版本的应用程序可以使用 D3DSAMP\_DMAPOFFSET D3DSAMPLERSTATETYPE 枚举来控制顶点中的偏移量到 presampled 的位移映射中的值。 在运行时映射用户模式下采样器状态 (D3DSAMP\_*Xxx*) 到内核模式 D3DTSS\_*Xxx*值，以便 DirectX 9.0 和更高版本的驱动程序不需要处理用户模式下采样器状态。 因此，驱动程序必须改为处理 D3DTSS\_DMAPOFFSET 中的值**TSState**的成员[ **D3DHAL\_DP2TEXTURESTAGESTATE** ](https://msdn.microsoft.com/library/windows/hardware/ff545878)D3DDP2OP 结构\_TEXTURESTAGESTATE 操作。 有关 D3DSAMPLERSTATETYPE 和 presampled 的位移映射的详细信息，请参阅最新的 DirectX SDK 文档。

 

 

 





