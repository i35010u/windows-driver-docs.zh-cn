---
title: 像素着色器
description: 像素着色器
ms.assetid: a44c5ee8-e9a7-4f9a-9547-e0c5ae49b82c
keywords:
- 像素着色器 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a015bfce0079029280901751f89061e52c9b622
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565553"
---
# <a name="pixel-shaders"></a>像素着色器


## <span id="ddk_pixel_shaders_gg"></span><span id="DDK_PIXEL_SHADERS_GG"></span>


支持 DirectX 8.0 DDI 的所有驱动程序可能支持新的 DP2 令牌 D3DDP2OP\_SETPIXELSHADER 如果可编程像素着色器支持硬件中。

D3DDP2OP\_SETPIXELSHADER 可用于通知当前的可编程像素着色器，若要使用的句柄的驱动程序。 像素着色器句柄是指通过 D3DDP2OP 以前创建的可编程像素着色器句柄\_CREATEPIXELSHADER DP2 令牌。

 

 





