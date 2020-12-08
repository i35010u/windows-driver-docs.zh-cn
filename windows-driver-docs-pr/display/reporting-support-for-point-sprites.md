---
title: 报告点精灵支持
description: 报告点精灵支持
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，点子画面
- point sprite WDK DirectX 8。0
- 大小 WDK 点子画面
- 点大小 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 560a49954a240c3b201d308a7319faad072a758a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786863"
---
# <a name="reporting-support-for-point-sprites"></a>报告点精灵支持


## <span id="ddk_reporting_support_for_point_sprites_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_POINT_SPRITES_GG"></span>


驱动程序通过将 D3DCAPS8 结构的 MaxPointSize 字段设置为大于1的浮点数，将结构的 " **MaxPointSize** " 字段设置为一个大于 (1 的浮点数，以指示 DX8 level) 的要求之一。 此值指定呈现目标像素中的最大点宽度和高度。 不支持点 sprite 的设备可将此值设置为1.0。

可以通过新的每顶点元素或新的呈现状态指定点子画面的大小。 如果驱动程序和硬件组合支持将点大小信息与其他顶点数据交错 (而不只是通过点大小渲染状态 D3DRS \_ POINTSIZE) ，则它应 \_ 在 FVFCaps 结构的 **D3DCAPS8** 字段中设置 D3DFVFCAPS PSIZE 标志。

缺少 D3DFVFCAPS \_ PSIZE 表示设备不支持在点大小中指定的顶点格式 (由 D3DFVF \_ PSIZE 标志指示) ; 因此，基本点大小始终是通过 D3DRS \_ POINTSIZE render 状态指定的。

尚未设置 D3DFVFCAPS PSIZE 标记的 DX8 驱动程序 \_ 仍需要接受 D3DFVF \_ PSIZE，并且必须忽略通过灵活顶点格式传递的任何点大小数据 (FVF) 。 请注意， \_ 必须为要用于呈现点子画面的顶点缓冲区设置 D3DUSAGE 点标志。 如果设置了此标志，则驱动程序可以避免在读取到 CPU 时速度缓慢的内存中分配这些顶点缓冲区。

当使用用户剪辑平面时，点子画面就会面临挑战。 点子画面的特定硬件实现可能只会根据用户剪辑平面剪裁点子画面的实际顶点位置，而不是实际渲染的展开四个部分。 如果驱动程序和硬件组合可以支持按其实际计算大小（而非简单顶点位置）来剪裁点子画面，则 \_ 应在 D3DCAPS8 的 **PrimitiveMiscCaps** 字段中设置 D3DPMISCCAPS CLIPPLANESCALEDPOINTS 功能位。

执行转换和照明的 DX8 驱动程序 (即，提供硬件顶点处理) 负责正确的点动画实现。 DirectX 8.0 运行时不执行任何模拟。 这意味着，即使硬件用于软件顶点处理，点 sprite 也是 DX8 驱动程序的责任。 但是，在 DirectX 8.1 和更高版本中，如果硬件用于软件顶点处理，则运行时可以提供模拟。

 

 





