---
title: Direct3D DDI
description: Direct3D DDI
ms.assetid: 5b6f7c06-7f54-4fc4-9b94-5fb425b5b3c8
keywords:
- Direct3D WDK Windows 2000 显示
- Direct3D WDK Windows 2000 显示，相关 Direct3D 信息
- 显示图形 WDK Windows 2000
- DDI WDK Direct3D
- 标头文件 WDK Direct3D
- Direct3D WDK Windows 2000 显示，标头文件
- 显示器驱动程序模型 WDK Windows 2000 Direct3D
- Windows 2000 显示器驱动程序模型 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 992732431b885822997f7ac21afa063c1d036a08
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563463"
---
# <a name="direct3d-ddi"></a>Direct3D DDI


## <span id="ddk_direct3d_gg"></span><span id="DDK_DIRECT3D_GG"></span>


Microsoft Direct3D 设备驱动程序接口 (DDI) 是一个图形界面，使供应商提供的 Direct3D 硬件加速。 接口是灵活，允许供应商提供的硬件功能根据 Direct3D 加速功能。 驱动程序编写人员实现 Direct3D DDI 显示器驱动程序的过程中不可或缺。

本部分介绍了 Direct3D DDI 和 Direct3D 驱动程序编写人员提供实现指导原则。 假定读者熟悉 Direct3D 和 Microsoft DirectDraw Api，并且读取器具有牢固掌握的 Windows 2000 显示器驱动程序模型，包括 DirectDraw DDI。

必须符合所有 Direct3D 驱动程序适用于 Windows 2000 及更高版本的 Microsoft DirectX 7.0 或更高版本的 Direct3D 驱动程序模型。 在 Microsoft Windows XP 中支持的 DirectX 8.0 驱动程序模型。

对于要创建 Microsoft Direct3D 驱动程序适用于 Microsoft Windows 2000 及更高版本的驱动程序编写人员应使用以下标头文件：

<span id="D3DNTHAL.H"></span>*d3dnthal.h*  
包含用于驱动程序级别结构由驱动程序实现的回调的原型和定义。 [ **D3DHAL\_DP2OPERATION** ](https://msdn.microsoft.com/library/windows/hardware/ff545678)此文件中定义枚举的类型。 中包括此标头*winddi.h*，其中必须包括在所有 Windows 2000 和更高版本显示驱动程序。

<span id="D3DTYPES.H"></span>*d3dtypes.h*  
包含应用程序和驱动程序使用的 Direct3D 类型定义。 除了 D3DHAL\_DP2OPERATION、 枚举的类型定义此标头中的所有其他 Direct3D。

<span id="D3DCAPS.H"></span>*d3dcaps.h*  
包含结构和描述的 Direct3D 驱动程序的各个方面的功能的定义。

<span id="DX95TYPE.H"></span>*dx95type.h*  
允许驱动程序开发人员能够编写可移植之间 Windows 2000 及更高版本和 Windows 98 的驱动程序代码 / me 一起提供。

<span id="DDRAWINT.H"></span>*ddrawint.h*  
此标头文件中，后者纳入*winddi.h*，需开发显示器驱动程序的 Microsoft DirectDraw 部分。

所有这些标头文件附带的与 Windows Driver Kit (WDK)。 以前的驱动程序开发工具包 (Ddk) 还提供了 Direct3D 驱动程序中的示例代码*Perm3*视频显示目录。

**请注意**   Microsoft Windows Driver Kit (WDK) 不包含 3Dlabs Permedia2 (*3dlabs.htm*) 和 3Dlabs Permedia3 (*Perm3.htm* ) 示例显示器驱动程序。 可以从 Windows Server 2003 SP1 DDK，可以从 DDK-WDHC 网站的 Windows 驱动程序开发工具包页面下载来获取这些示例驱动程序。

 

引用页的 Direct3D DDI 函数、 结构和枚举可在[Direct3D 驱动程序函数](https://msdn.microsoft.com/library/windows/hardware/ff552853)， [Direct3D 驱动程序结构](https://msdn.microsoft.com/library/windows/hardware/ff552858)，和[Direct3D 驱动程序枚举](https://msdn.microsoft.com/library/windows/hardware/ff552850).

与 SDK 相关的 Direct3D 接口方面主要参考是 Microsoft Windows SDK 文档。 *计算机图形中：原则和实践*Foley、 van 坝、 Feiner 和 Hughes，由 Addison-wesley 发布，是有用的常规图形引用。

 

 





