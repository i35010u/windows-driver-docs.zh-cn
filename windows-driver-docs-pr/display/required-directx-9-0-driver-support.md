---
title: 所需的 DirectX 9.0 驱动程序支持
description: 所需的 DirectX 9.0 驱动程序支持
ms.assetid: 9bc68101-c1be-470c-9eb7-9a689a2dd47c
keywords:
- 必需的驱动程序支持 WDK DirectX 9。0
- DirectX 9.0 驱动程序支持 WDK
ms.date: 11/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: f3be2fed7d33803a74f2156b6fd0957e69a6d3fc
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825887"
---
# <a name="required-directx-90-driver-support"></a>所需的 DirectX 9.0 驱动程序支持

如果显示驱动程序为 DirectX 7.0 或更高版本的驱动程序，DirectX 9.0 运行时将提供硬件加速。 但是，要使操作系统作为9.0 版驱动程序加载的驱动程序，该驱动程序必须实现以下部分中所述的功能：

- [支持二维操作](supporting-two-dimensional-operations.md)

- [支持动态资源](supporting-dynamic-resources.md)

- [支持顶点着色器声明](supporting-vertex-shader-declarations.md)

- [支持流偏移](supporting-stream-offsets.md)

- [报告支持 UBYTE4 顶点元素](reporting-support-of-ubyte4-vertex-element.md)

- [用于设置呈现目标的支持命令](supporting-commands-for-setting-render-target.md)

- [设置剪刀矩形](setting-scissor-rectangle.md)

- [通知 DirectX 版本](notifying-about-directx-version.md)

- [报告 DDI 版本](reporting-ddi-version.md)

DirectX 9.0 版本驱动程序必须支持：

-   通过在请求时返回 D3DCAPS9 结构来报告其设备的功能。 驱动程序将返回 D3DCAPS9 结构，以响应使用 D3DGDI2\_类型\_GETD3DCAPS9 值的**GetDriverInfo2**请求，类似于返回 D3DCAPS8 结构，如[报告 DirectX 8.0 样式 Direct3D 中所述。功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 支持[GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此请求的支持。 D3DCAPS9 包含 DirectX 9.0 和 DirectX 8.0 相关功能。<br/><br/>在 DirectX 8.0 运行时查询时，驱动程序必须继续仅报告 D3DCAPS8 中的 DirectX 8.0 相关功能。

-   在[**DDPIXELFORMAT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的**dwOperations**成员中，将 D3DFORMAT\_OP\_BUMPMAP 标志设置为可以支持固定函数或可编程像素管道中的凹凸映射的所有表面格式。

-   报告[异步查询操作的支持](supporting-asynchronous-query-operations.md)，即使驱动程序只是指示不支持任何查询类型，也是如此。 有关详细信息，请参阅[验证对查询类型的支持](verifying-support-of-query-types.md)。<br/><br/>异步查询会对[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) DDI 施加两个新的要求。 有关详细信息，请参阅对[D3DDRAWPRIMITIVES2 DDI 施加要求](imposing-requirements-on-the-d3ddrawprimitives2-ddi.md)。

-   让应用程序执行[具有繁忙的现有队列的其他处理](processing-with-busy-present-queues.md)。
