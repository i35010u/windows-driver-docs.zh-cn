---
title: Direct3D DDI
description: Direct3D DDI
keywords:
- Direct3D WDK Windows 2000 显示
- Direct3D WDK Windows 2000 显示，关于 Direct3D
- 图形 WDK Windows 2000 显示
- DDI WDK Direct3D
- 头文件 WDK Direct3D
- Direct3D WDK Windows 2000 显示，头文件
- 显示驱动程序模型 WDK Windows 2000，Direct3D
- Windows 2000 显示器驱动程序模型 WDK，Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbf11cea0ffcca11f35fa09cffe7b49c89ae0f57
ms.sourcegitcommit: 6b3358fb2e5328c2699b349f1e6ff8b804cc3b35
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2021
ms.locfileid: "98069401"
---
# <a name="direct3d-ddi"></a>Direct3D DDI

 (DDI) 使用 Microsoft Direct3D 设备驱动程序接口，它是一种图形界面，允许供应商提供 Direct3D 的硬件加速。 接口非常灵活，允许供应商根据硬件功能提供 Direct3D 加速功能。 驱动程序编写器将 Direct3D DDI 作为显示驱动程序的组成部分来实现。

本部分介绍 Direct3D DDI，并为 Direct3D 驱动程序编写器提供实现准则。 假设读者熟悉 Direct3D 和 Microsoft DirectDraw Api，并且读者对 Windows 2000 显示器驱动程序模型（包括 DirectDraw DDI）进行了全面的了解。

适用于 Windows 2000 和更高版本的所有 Direct3D 驱动程序必须符合 Microsoft DirectX 7.0 或更高版本的 Direct3D 驱动程序模型。 Microsoft Windows XP 支持 DirectX 8.0 驱动程序模型。

正在为 Microsoft Windows 2000 和更高版本创建 Microsoft Direct3D 驱动程序的驱动程序编写器应使用以下头文件：

[*d3dhal*](/windows-hardware/drivers/ddi/d3dhal)  
包含由驱动程序和驱动程序级别的结构的定义实现的回调的原型。 此文件中定义了 [**D3DHAL_DP2OPERATION**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation) 枚举类型。 此标头包含在 *winddi* 中，此标头必须包含在所有 Windows 2000 和更高版本的驱动程序中。

[*d3d9types*](/windows-hardware/drivers/ddi/d3d9types) 包含应用程序和驱动程序使用的 Direct3D 类型定义。 除 D3DHAL_DP2OPERATION 之外，此标头中定义了所有其他 Direct3D 枚举类型。

[*d3dcaps*](/windows-hardware/drivers/ddi/d3dcaps) 包含描述 Direct3D 驱动程序各个方面功能的结构和定义。

*ddrawint*  
此标头文件包含在 *winddi* 中，是开发显示驱动程序的 Microsoft DirectDraw 部分所必需的。

所有这些头文件随 Windows 驱动程序工具包一起提供 (WDK) 。 以前的驱动程序开发工具包 (Ddk) 也提供 *Perm3* 视频显示目录中 Direct3D 驱动程序的示例代码。

Microsoft Windows 驱动程序工具包 (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs *Permedia3 (Perm3.htm) 示例* 显示驱动程序。 你可以从 Windows Server 2003 SP1 DDK 获取这些示例驱动程序，你可以从 WDHC 网站的 "DDK-Windows 驱动程序开发工具包" 页下载该驱动程序。

Direct3D 接口的 SDK 相关方面的主要参考是 Microsoft Windows SDK 文档。 *计算机图形：* 按 Foley、van Dam、Feiner 和 Hughes （由 Addison-Wesley 发布）的原则和实践是一项有用的通用图形引用。
