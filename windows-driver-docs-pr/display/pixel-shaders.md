---
title: 像素着色器
description: 像素着色器
keywords:
- 象素着色器 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aeafcb4507dcdf624a4617476ae77d845818c681
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838045"
---
# <a name="pixel-shaders"></a>像素着色器


## <span id="ddk_pixel_shaders_gg"></span><span id="DDK_PIXEL_SHADERS_GG"></span>


\_如果硬件支持可编程像素着色，则支持 DirectX 8.0 DDI 的所有驱动程序都可能支持新的 DP2 TOKEN D3DDP2OP SETPIXELSHADER。

D3DDP2OP \_ SETPIXELSHADER 可用于通知驱动程序要使用的当前可编程像素着色器的句柄。 像素着色器句柄是指先前通过 D3DDP2OP CREATEPIXELSHADER DP2 标记创建的可编程像素着色器句柄 \_ 。

 

 





