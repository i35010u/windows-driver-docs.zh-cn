---
title: DirectX 8.0 驱动程序的最低功能要求
description: DirectX 8.0 驱动程序的最低功能要求
ms.assetid: 8c939013-516c-4048-8de5-e95529891ac9
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，请报告功能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1368535cadc96b5c9b00561c1449426c2a501189
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385027"
---
# <a name="minimum-capability-requirements-for-directx-80-drivers"></a>DirectX 8.0 驱动程序的最低功能要求


## <span id="ddk_minimum_capability_requirements_for_directx_8_0_drivers_gg"></span><span id="DDK_MINIMUM_CAPABILITY_REQUIREMENTS_FOR_DIRECTX_8_0_DRIVERS_GG"></span>


除了在响应中返回 D3DCAPS8 数据结构**GetDriverInfo2**查询中，DirectX 8.0 运行时有一个驱动程序必须满足才能被视为 DirectX 8.0 级别驱动程序的其他要求。

DirectX 8.0 驱动程序必须显式：

-   报告中的一个或多个顶点流支持**MaxStreams** D3DCAPS8 字段。

-   报告在至少一个中的最大点子画面大小**MaxPointSize** D3DCAPS8 字段。

-   修改它的支持的纹理格式，以支持新样式像素格式规范的列表。

-   处理新[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) (DP2) 绘制标记。

-   处理[ **D3dCreateSurfaceEx** ](https://msdn.microsoft.com/library/windows/hardware/ff542840)顶点和索引缓冲区即使您的驱动程序不支持的视频内存顶点缓冲区创建的。 对系统内存顶点和索引缓冲区句柄传递给驱动程序。

-   设置新 posttransformed 的剪辑标志 D3DPMISCCAPS\_CLIPTLVERT 如果硬件支持的剪辑 posttransformed 顶点数据。

应注意的是驱动程序不需要支持 DirectX 8.0 的新功能，如像素或顶点着色器，体积纹理的任何点 sprite （超过了非零值的最大点）、 多重采样或甚至多个顶点流 （如可能是驱动程序设置为一个同时顶点流的最大数目） 才能被视为 DirectX 8.0 驱动程序。

 

 





