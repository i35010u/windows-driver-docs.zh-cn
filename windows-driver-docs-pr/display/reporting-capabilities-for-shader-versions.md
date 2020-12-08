---
title: 报告着色器版本的功能
description: 报告着色器版本的功能
keywords:
- 着色器 WDK DirectX 9。0
- 顶点着色器 WDK DirectX 9。0
- 象素着色器 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56f4a1a806c1b52a3efe651cc01101dfc401b79e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783973"
---
# <a name="reporting-capabilities-for-shader-versions"></a>报告着色器版本的功能


## <span id="ddk_reporting_capabilities_for_shader_versions_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_VERSIONS_GG"></span>


支持像素或顶点着色器版本2.0 或3.0 及更高版本的显示设备的 DirectX 9.0 版本驱动程序必须指示它支持最小的一组功能，以便将设备绑定到着色器版本。 驱动程序必须将 D3DCAPS9 结构的成员设置为表示支持功能。 驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。 以下主题介绍了这些功能：

[报告着色器 2 支持功能](reporting-capabilities-for-shader-2-support.md)

[报告着色器 3 支持功能](reporting-capabilities-for-shader-3-support.md)

 

 





