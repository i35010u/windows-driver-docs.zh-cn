---
title: 处理体积纹理的创建
description: 处理体积纹理的创建
ms.assetid: d5f521df-cd52-4c7e-9ad2-5df343c96e8c
keywords:
- 纹理 WDK DirectX 8.0
- DirectX 8.0 发行说明 WDK Windows 2000 显示，体积纹理
- 体积纹理 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51953060e48bd859b438e6490123a80a8595ee96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369851"
---
# <a name="handling-the-creation-of-volume-textures"></a>处理体积纹理的创建


## <span id="ddk_handling_the_creation_of_volume_textures_gg"></span><span id="DDK_HANDLING_THE_CREATION_OF_VOLUME_TEXTURES_GG"></span>


DirectX 8.0 引入了一个新图面上功能位 DDSCAPS2\_卷。 设置此标志**ddsCapsEx.dwCaps2**字段的面[ **DD\_图面\_详细**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_more)结构。 在中[ *DdCreateSurface* ](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))并[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)回调卷纹理的深度中的低位字**dwCaps4**图面上的扩展功能的字段 (**ddsCapsEx**) 的表面的 DD\_图面\_更多结构。 该驱动程序应返回"切片间距"（，即要添加将从一个 2D 切片的数据量移动到下一步的字节数） 中的卷纹理**dwBlockSizeY**字段的图面上的全局结构。

 

 





