---
title: 报告着色器版本的功能
description: 报告着色器版本的功能
ms.assetid: a82ac539-1386-417a-a64f-0a7ddc6d28d9
keywords:
- 着色器 WDK DirectX 9.0
- 顶点着色器 WDK DirectX 9.0
- 像素着色器 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5db7ce746ff7868b7535b2bee67a96924c065a41
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383281"
---
# <a name="reporting-capabilities-for-shader-versions"></a>报告着色器版本的功能


## <span id="ddk_reporting_capabilities_for_shader_versions_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_VERSIONS_GG"></span>


显示设备支持像素或顶点着色器版本 2.0 或 3.0 及更高版本的 DirectX 9.0 版本驱动程序必须指示它支持小以便将其绑定到着色器版本的设备的功能集。 该驱动程序必须设置 D3DCAPS9 结构的成员来指示支持的功能。 该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。 以下主题中讨论了这些功能：

[对着色器 2 支持的报告功能](reporting-capabilities-for-shader-2-support.md)

[对着色器 3 支持报告功能](reporting-capabilities-for-shader-3-support.md)

 

 





