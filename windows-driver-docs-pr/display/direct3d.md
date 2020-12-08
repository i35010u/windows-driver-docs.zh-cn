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
ms.openlocfilehash: 6eab520248e77843c656e204a20fafe213cebda3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809417"
---
# <a name="direct3d-ddi"></a>Direct3D DDI


## <span id="ddk_direct3d_gg"></span><span id="DDK_DIRECT3D_GG"></span>


 (DDI) 使用 Microsoft Direct3D 设备驱动程序接口，它是一种图形界面，允许供应商提供 Direct3D 的硬件加速。 接口非常灵活，允许供应商根据硬件功能提供 Direct3D 加速功能。 驱动程序编写器将 Direct3D DDI 作为显示驱动程序的组成部分来实现。

本部分介绍 Direct3D DDI，并为 Direct3D 驱动程序编写器提供实现准则。 假设读者熟悉 Direct3D 和 Microsoft DirectDraw Api，并且读者对 Windows 2000 显示器驱动程序模型（包括 DirectDraw DDI）进行了全面的了解。

适用于 Windows 2000 和更高版本的所有 Direct3D 驱动程序必须符合 Microsoft DirectX 7.0 或更高版本的 Direct3D 驱动程序模型。 Microsoft Windows XP 支持 DirectX 8.0 驱动程序模型。

正在为 Microsoft Windows 2000 和更高版本创建 Microsoft Direct3D 驱动程序的驱动程序编写器应使用以下头文件：

<span id="D3DNTHAL.H"></span>*d3dnthal*  
包含由驱动程序和驱动程序级别的结构的定义实现的回调的原型。 [**D3DHAL \_ DP2OPERATION**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)枚举类型是在此文件中定义的。 此标头包含在 *winddi* 中，此标头必须包含在所有 Windows 2000 和更高版本的驱动程序中。

<span id="D3DTYPES.H"></span>*d3dtypes*  
包含应用程序和驱动程序使用的 Direct3D 类型定义。 除了 D3DHAL \_ DP2OPERATION，所有其他 Direct3D 枚举类型都在此标头中定义。

<span id="D3DCAPS.H"></span>*d3dcaps*  
包含描述 Direct3D 驱动程序各个方面的功能的结构和定义。

<span id="DX95TYPE.H"></span>*dx95type*  
允许驱动程序开发人员编写可在 Windows 2000 和更高版本以及 Windows 98/Me 之间移植的驱动程序代码。

<span id="DDRAWINT.H"></span>*ddrawint*  
此标头文件包含在 *winddi* 中，是开发显示驱动程序的 Microsoft DirectDraw 部分所必需的。

所有这些头文件随 Windows 驱动程序工具包一起提供 (WDK) 。 以前的驱动程序开发工具包 (Ddk) 也提供 *Perm3* 视频显示目录中 Direct3D 驱动程序的示例代码。

**注意**   Microsoft Windows 驱动程序工具包 (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs *Permedia3 (Perm3.htm) 示例* 显示驱动程序。 你可以从 Windows Server 2003 SP1 DDK 获取这些示例驱动程序，你可以从 WDHC 网站的 "DDK-Windows 驱动程序开发工具包" 页下载该驱动程序。

 

Direct3d DDI 函数、结构和枚举的参考页可以在 [Direct3d 驱动程序函数](/windows-hardware/drivers/ddi/index)、 [Direct3d 驱动程序结构](/windows-hardware/drivers/ddi/index)和 [Direct3D 驱动程序枚举](/windows-hardware/drivers/ddi/index)中找到。

Direct3D 接口的 SDK 相关方面的主要参考是 Microsoft Windows SDK 文档。 *计算机图形：* 按 Foley、van Dam、Feiner 和 Hughes （由 Addison-Wesley 发布）的原则和实践是一项有用的通用图形引用。

 

