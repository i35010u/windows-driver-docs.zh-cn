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
ms.openlocfilehash: a791e32ca3954acee0b1e49f52f56d76959968fd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838950"
---
# <a name="enumerating-dxt-formats"></a>枚举 DXT 格式


## <span id="ddk_enumerating_dxt_formats_gg"></span><span id="DDK_ENUMERATING_DXT_FORMATS_GG"></span>


在 Microsoft DirectX 中，驱动程序可以通过两种方式来枚举像素格式。 第一种方法枚举可用于纹理的格式。 此方法是使用[**D3DHAL\_GLOBALDRIVERDATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)结构的**lpTextureFormats**成员实现的。 第二个方法枚举可用于 DDSCAPS 的格式\_覆盖面或 DDSCAPS\_OFFSCREENPLAIN 图面。 第二种方法使用[**dd\_HALINFO**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构中包含的[**DDCORECAPS**](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构的**DWNUMFOURCCCODES**成员以及 dd\_HALINFO 结构中也包含的**lpdwFourCC**数组。

因为 DXT 格式主要用于用作纹理，所以，驱动程序仅通过第一种方法枚举 DXT 格式。 不需要将 DXT 格式添加到**lpdwFourCC**数组。

 

 





