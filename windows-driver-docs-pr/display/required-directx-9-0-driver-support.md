---
title: 所需的 DirectX 9.0 驱动程序支持
description: 所需的 DirectX 9.0 驱动程序支持
ms.assetid: 9bc68101-c1be-470c-9eb7-9a689a2dd47c
keywords:
- 必需的驱动程序支持 WDK DirectX 9.0
- DirectX 9.0 驱动程序支持 WDK
ms.date: 11/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: b97afe7f85863a658838384ef0a98071b513597a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533020"
---
# <a name="required-directx-90-driver-support"></a>所需的 DirectX 9.0 驱动程序支持

如果显示驱动程序是 DirectX 7.0 或更高版本的驱动程序，DirectX 9.0 运行时将提供硬件加速。 但是，若要加载的 9.0 版驱动程序作为操作系统的驱动程序，它必须实现以下各节所述的功能：

- [支持二维操作](supporting-two-dimensional-operations.md)

- [支持动态资源](supporting-dynamic-resources.md)

- [支持的顶点着色器声明](supporting-vertex-shader-declarations.md)

- [支持 Stream 偏移量](supporting-stream-offsets.md)

- [报告支持 UBYTE4 顶点元素](reporting-support-of-ubyte4-vertex-element.md)

- [设置呈现器目标的支持的命令](supporting-commands-for-setting-render-target.md)

- [设置剪刀矩形](setting-scissor-rectangle.md)

- [有关 DirectX 版本通知](notifying-about-directx-version.md)

- [报告 DDI 版本](reporting-ddi-version.md)

必须支持 DirectX 9.0 版本驱动程序：

-   通过返回请求时的 D3DCAPS9 结构报告其设备的功能。 该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**请求使用 D3DGDI2\_类型\_GETD3DCAPS9 值类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此请求的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。 D3DCAPS9 包含 DirectX 9.0 和 DirectX 8.0 相关功能。<br/><br/>该驱动程序必须继续报告仅 DirectX 8.0 相关中 D3DCAPS8 DirectX 8.0 运行时进行查询时的功能。

-   设置 D3DFORMAT\_OP\_BUMPMAP 标志**dwOperations**的成员[ **DDPIXELFORMAT** ](https://msdn.microsoft.com/library/windows/hardware/ff550274)对所有图面上格式结构可以在固定函数或可编程像素管道支持凹凸贴图。

-   Reporting[对异步查询操作的支持](supporting-asynchronous-query-operations.md)，即使该驱动程序只是响应通过指示不支持任何查询类型。 有关详细信息，请参阅[验证查询类型支持](verifying-support-of-query-types.md)。<br/><br/>异步查询实施两个新的要求[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704) DDI。 有关详细信息，请参阅[D3dDrawPrimitives2 DDI 的实施要求](imposing-requirements-on-the-d3ddrawprimitives2-ddi.md)。

-   让应用程序执行其他[忙存在队列处理](processing-with-busy-present-queues.md)。
