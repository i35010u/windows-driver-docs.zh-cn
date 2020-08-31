---
title: DirectX 8.0 驱动程序的最低功能要求
description: DirectX 8.0 驱动程序的最低功能要求
ms.assetid: 8c939013-516c-4048-8de5-e95529891ac9
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，报告功能
- D3DCAPS8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a2c5af1685baab7ac3c5e9e84022169866668e5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066498"
---
# <a name="minimum-capability-requirements-for-directx-80-drivers"></a>DirectX 8.0 驱动程序的最低功能要求


## <span id="ddk_minimum_capability_requirements_for_directx_8_0_drivers_gg"></span><span id="DDK_MINIMUM_CAPABILITY_REQUIREMENTS_FOR_DIRECTX_8_0_DRIVERS_GG"></span>


除了返回 D3DCAPS8 数据结构以响应 **GetDriverInfo2** 查询，DirectX 8.0 运行时还具有驱动程序必须满足的其他要求，以将其视为 DirectX 8.0 级别驱动程序。

DirectX 8.0 驱动程序必须显式：

-   针对 D3DCAPS8 的 **MaxStreams** 字段中的一个或多个顶点流的报表支持。

-   在 D3DCAPS8 的 **MaxPointSize** 字段中报告至少一个子画面大小的最大点动画大小。

-   修改其支持的纹理格式列表，以支持新的样式像素格式规范。

-   处理新的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) (DP2) 绘制标记。

-   处理顶点和索引缓冲区的 [**D3dCreateSurfaceEx**](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) ，即使您的驱动程序不支持视频内存顶点缓冲区创建也是如此。 系统内存顶点和索引缓冲区的句柄传递给驱动程序。

-   \_如果硬件支持 posttransformed 顶点数据的剪辑，请设置新的 posttransformed 剪切标志 D3DPMISCCAPS CLIPTLVERT。

应注意的是，驱动程序不需要支持 DirectX 8.0 的任何新功能，如像素或顶点着色器、音量纹理、点 sprite (超出非零最大点大小) 、多级（或甚至多个顶点 (流），因为驱动程序可以将同时进行的顶点流的最大数目设置为一个) ，以便被视为 DirectX 8.0 驱动程序。

 

