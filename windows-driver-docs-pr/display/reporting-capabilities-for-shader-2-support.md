---
title: 报告着色器 2 支持功能
description: 报告着色器 2 支持功能
keywords:
- 着色器 WDK DirectX 9.0，着色器2.0 支持
- 顶点着色器 WDK DirectX 9.0，着色器2.0 支持
- 象素着色器 WDK DirectX 9.0，着色器2.0 支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7ea4197e966d8c478a9219036a0b699525d9580
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783979"
---
# <a name="reporting-capabilities-for-shader-2-support"></a>报告着色器 2 支持功能


## <span id="ddk_reporting_capabilities_for_shader_2_support_gg"></span><span id="DDK_REPORTING_CAPABILITIES_FOR_SHADER_2_SUPPORT_GG"></span>


支持像素或顶点着色器版本2.0 及更高版本的显示设备的 DirectX 9.0 版本驱动程序必须指出它支持以下功能：

如果设备支持顶点着色器2.0 及更高版本，则其驱动程序必须将 D3DCAPS9 结构的成员设置为以下值：

-   将 **MaxStreams** 成员设置为至少8，以指示设备可处理8个或更多并发数据流。

-   将 \_ **DeclTypes** 成员中的 D3DDTCAPS UBYTE4 位设置为1，以指示对 UBYTE4 顶点元素类型的支持。 有关详细信息，请参阅 [报表支持 UBYTE4 顶点元素](reporting-support-of-ubyte4-vertex-element.md)。

如果设备支持像素着色器2.0 及更高版本，则其驱动程序必须在 **TextureCaps** 成员中配置以下位，以指示驱动程序是否支持将二维纹理映射作为条件或无条件的 nonpowers。 有关详细信息，请参阅 [**D3DPRIMCAPS**](/windows-hardware/drivers/ddi/d3dcaps/ns-d3dcaps-_d3dprimcaps) 参考页中对这些位的说明。

-   将 D3DPTEXTURECAPS \_ POW2 和 D3DPTEXTURECAPS \_ NONPOW2CONDITIONAL 位设置为1，以指示条件支持。

-   将 D3DPTEXTURECAPS \_ POW2 和 D3DPTEXTURECAPS \_ NONPOW2CONDITIONAL 位设置为 0 (也就是说，不要设置这些位) 以指示无条件支持。

 

