---
title: 报告点精灵支持
description: 报告点精灵支持
ms.assetid: 57241e2d-a636-454b-8497-17978b6ec285
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，点 sprite
- 点 sprite WDK DirectX 8.0
- 大小 WDK 点 sprite
- 点大小 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d53a5269e42e3dafebf50e83f91648f707caae11
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383247"
---
# <a name="reporting-support-for-point-sprites"></a>报告点精灵支持


## <span id="ddk_reporting_support_for_point_sprites_gg"></span><span id="DDK_REPORTING_SUPPORT_FOR_POINT_SPRITES_GG"></span>


驱动程序通过设置通知点 sprite 的支持的运行时**MaxPointSize** D3DCAPS8 结构为浮点数大于一 （报告的值为 1 以指示 DX8 要求的一部分的字段级别 HAL）。 此值以呈现器目标像素为单位指定的最大点宽度和高度。 不支持点 sprite 的设备可以将此值设置为 1.0。

可以通过新的每个顶点元素或通过新呈现状态指定点子画面的大小。 如果驱动程序和硬件组合支持交错点大小信息与其他顶点数据 (而不是只需通过点大小呈现状态 D3DRS\_POINTSIZE)，它应设置 D3DFVFCAPS\_中的 PSIZE 标志**FVFCaps** D3DCAPS8 结构的字段。

缺少 D3DFVFCAPS\_PSIZE 指示该设备不支持在点大小中指定的顶点格式 (由 D3DFVF\_PSIZE 标志); 因此，使用 D3DRS 始终指定基点大小\_POINTSIZE 呈现状态。

DX8 驱动程序为其 D3DFVFCAPS\_PSIZE 标志未设置仍然需要接受 D3DFVF\_PSIZE 和必须忽略通过灵活顶点格式 (FVF) 传递的任何点大小数据。 请注意，D3DUSAGE\_点标志必须为要用于呈现点 sprite 的顶点缓冲区设置。 如果设置此标志，该驱动程序可以避免分配这些顶点缓冲区中读取到 CPU 的速度较慢的内存类型。

使用用户剪辑平面时，点 sprite 带来了挑战。 它是可能的点 sprite 的特定硬件实现将剪辑仅针对用户剪裁平面，而不是实际呈现展开的四点 sprite 的实际顶点位置。 如果驱动程序和硬件组合可以通过其实际支持剪辑的点 sprite 计算大小而不是简单的顶点位置然后 D3DPMISCCAPS\_应设置 CLIPPLANESCALEDPOINTS 功能位**PrimitiveMiscCaps** D3DCAPS8 字段。

执行转换和照明的 DX8 驱动程序 （即，提供硬件顶点处理） 负责正确点子画面实现。 由 DirectX 8.0 运行时不执行任何模拟。 这意味着，即使在硬件与软件顶点处理一起使用，点 sprite DX8 驱动程序的责任。 但是，在 DirectX 8.1 及更高版本，如果硬件与软件顶点处理一起使用，在运行时可以提供仿真。

 

 





