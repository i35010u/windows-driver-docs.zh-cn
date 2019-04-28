---
title: 报告着色器 2 支持功能
description: 报告着色器 2 支持功能
ms.assetid: 27397e32-cdc0-47b5-b9b5-a4b22ed971f3
keywords:
- 着色器 WDK DirectX 9.0，着色器 2.0 支持
- 顶点着色器 WDK DirectX 9.0，着色器 2.0 支持
- 像素着色器 WDK DirectX 9.0，着色器 2.0 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c3f28a32013795f70d9bb5d6b32150d0a73586d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350217"
---
# <a name="reporting-capabilities-for-shader-2-support"></a>报告着色器 2 支持功能


## <span id="ddk_reporting_capabilities_for_shader_2_support_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_2_SUPPORT_GG"></span>


显示设备支持像素或顶点着色器版本 2.0 及更高版本的 DirectX 9.0 版本驱动程序必须指示它支持以下功能：

如果设备支持顶点着色器 2.0 及更高版本，其驱动程序必须设置为以下值 D3DCAPS9 结构的成员：

-   设置**MaxStreams**成员为至少 8 指示设备可以处理 8 或更多的并发数据流。

-   设置 D3DDTCAPS\_UBYTE4 位**DeclTypes**为 1 的成员来指示 UBYTE4 顶点元素类型的支持。 有关详细信息，请参阅[报告支持的 UBYTE4 顶点元素](reporting-support-of-ubyte4-vertex-element.md)。

如果设备支持像素着色器 2.0 以及更高版本，其驱动程序必须配置中的以下位**TextureCaps**成员以指示驱动程序是否支持有条件地或无条件地 2-d 纹理映射作为 nonpowers 2. 有关详细信息，请参阅中的这些说明[ **D3DPRIMCAPS** ](https://msdn.microsoft.com/library/windows/hardware/ff549034)参考页。

-   设置 D3DPTEXTURECAPS\_POW2 和 D3DPTEXTURECAPS\_NONPOW2CONDITIONAL 位为 1，表示有条件支持。

-   设置 D3DPTEXTURECAPS\_POW2 和 D3DPTEXTURECAPS\_NONPOW2CONDITIONAL 位为 0 （即，不应设置以下这些位） 来指示无条件的支持。

 

 





