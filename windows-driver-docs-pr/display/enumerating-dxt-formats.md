---
title: 枚举 DXT 格式
description: 枚举 DXT 格式
ms.assetid: 77fc961f-1b94-43c1-b238-86f7d8e96835
keywords:
- 绘制压缩纹理 WDK DirectDraw，枚举 DXT 格式
- DirectDraw 压缩纹理 WDK Windows 2000 显示，枚举 DXT 格式
- 压缩的纹理面 WDK DirectDraw，枚举 DXT 格式
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
- 枚举 DXT 格式 WDK DirectDraw
- DXT 格式 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c760a018a2fc23da75ea3c11e06e4a94d4187ba
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065864"
---
# <a name="enumerating-dxt-formats"></a>枚举 DXT 格式


## <span id="ddk_enumerating_dxt_formats_gg"></span><span id="DDK_ENUMERATING_DXT_FORMATS_GG"></span>


在 Microsoft DirectX 中，驱动程序可以通过两种方式来枚举像素格式。 第一种方法枚举可用于纹理的格式。 此方法是使用[**D3DHAL \_ GLOBALDRIVERDATA**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)结构的**lpTextureFormats**成员实现的。 第二个方法枚举可用于 DDSCAPS \_ 覆盖面或 DDSCAPS OFFSCREENPLAIN 图面的格式 \_ 。 第二种方法使用[**dd \_ HALINFO**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构中包含的[**DDCORECAPS**](/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**dwNumFourCCCodes**成员以及 Dd HALINFO 结构中也包含的**lpdwFourCC**数组 \_ 。

因为 DXT 格式主要用于用作纹理，所以，驱动程序仅通过第一种方法枚举 DXT 格式。 不需要将 DXT 格式添加到 **lpdwFourCC** 数组。

 

