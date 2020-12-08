---
title: 所需的 DirectX 9.0 驱动程序支持
description: 所需的 DirectX 9.0 驱动程序支持
keywords:
- 必需的驱动程序支持 WDK DirectX 9。0
- DirectX 9.0 驱动程序支持 WDK
ms.date: 11/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0e2f341d3a932bda4c9fb5361e7965afe33a8711
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808863"
---
# <a name="required-directx-90-driver-support"></a>所需的 DirectX 9.0 驱动程序支持

如果显示驱动程序为 DirectX 7.0 或更高版本的驱动程序，DirectX 9.0 运行时将提供硬件加速。 但是，要使操作系统作为9.0 版驱动程序加载的驱动程序，该驱动程序必须实现以下部分中所述的功能：

- [支持二维操作](supporting-two-dimensional-operations.md)

- [支持动态资源](supporting-dynamic-resources.md)

- [支持顶点着色器声明](supporting-vertex-shader-declarations.md)

- [支持流偏移量](supporting-stream-offsets.md)

- [报告 UBYTE4 顶点元素支持](reporting-support-of-ubyte4-vertex-element.md)

- [支持用于设置渲染器目标的命令](supporting-commands-for-setting-render-target.md)

- [设置裁切矩形](setting-scissor-rectangle.md)

- [DirectX 版本通知](notifying-about-directx-version.md)

- [报告 DDI 版本](reporting-ddi-version.md)

DirectX 9.0 版本驱动程序必须支持：

-   通过在请求时返回 D3DCAPS9 结构来报告其设备的功能。 驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 请求，使用 D3DGDI2 \_ 类型 \_ GETD3DCAPS9 值，类似于返回 D3DCAPS8 结构，如 [报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此请求的支持。 D3DCAPS9 包含 DirectX 9.0 和 DirectX 8.0 相关功能。<br/><br/>在 DirectX 8.0 运行时查询时，驱动程序必须继续仅报告 D3DCAPS8 中的 DirectX 8.0 相关功能。

-   在 \_ \_ [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的 **DWOPERATIONS** 成员中，将 D3DFORMAT OP BUMPMAP 标志设置为可以支持固定函数或可编程像素管道中的凹凸映射的所有表面格式。

-   报告 [异步查询操作的支持](supporting-asynchronous-query-operations.md)，即使驱动程序只是指示不支持任何查询类型，也是如此。 有关详细信息，请参阅 [验证对查询类型的支持](verifying-support-of-query-types.md)。<br/><br/>异步查询会对 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI 施加两个新的要求。 有关详细信息，请参阅对 [D3DDRAWPRIMITIVES2 DDI 施加要求](imposing-requirements-on-the-d3ddrawprimitives2-ddi.md)。

-   让应用程序执行 [具有繁忙的现有队列的其他处理](processing-with-busy-present-queues.md)。
