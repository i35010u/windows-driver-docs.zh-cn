---
title: 枚举 DXT 格式
description: 枚举 DXT 格式
ms.assetid: 77fc961f-1b94-43c1-b238-86f7d8e96835
keywords:
- 绘制压缩的纹理 WDK DirectDraw，枚举 DXT 格式
- DirectDraw 压缩的纹理 WDK Windows 2000 显示，枚举 DXT 格式
- 压缩的纹理图面 WDK DirectDraw，枚举 DXT 格式
- WDK DirectDraw，压缩的纹理的图面
- 纹理 WDK DirectDraw 压缩
- 枚举 DXT 格式 WDK DirectDraw
- DXT 格式 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 83468541367396667d95762aeed2e791beb30c60
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355550"
---
# <a name="enumerating-dxt-formats"></a>枚举 DXT 格式


## <span id="ddk_enumerating_dxt_formats_gg"></span><span id="DDK_ENUMERATING_DXT_FORMATS_GG"></span>


Microsoft DirectX 中有两种驱动程序以枚举像素格式的方法。 第一种方法枚举可用于纹理的格式。 此方法使用实现**lpTextureFormats**的成员[ **D3DHAL\_GLOBALDRIVERDATA** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_globaldriverdata)结构。 第二种方法枚举可用于任一 DDSCAPS 的格式\_覆盖面或 DDSCAPS\_OFFSCREENPLAIN 图面。 第二种方法使用**dwNumFourCCCodes**的成员[ **DDCORECAPS** ](https://docs.microsoft.com/windows/desktop/api/ddrawi/ns-ddrawi-_ddcorecaps)结构中包含[ **DD\_HALINFO** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_halinfo)结构并**lpdwFourCC**数组，其中也包含在 DD\_HALINFO 结构。

DXT 格式主要是为了用作纹理，因为您的驱动程序只能通过第一种方法枚举 DXT 格式。 无需添加到 DXT 格式**lpdwFourCC**数组。

 

 





