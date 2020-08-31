---
title: 将图面设为 FOURCC 格式
description: 将图面设为 FOURCC 格式
ms.assetid: 947b73c9-3f1d-485e-9966-815b40a06342
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，纹理格式列表
- 纹理格式列出 WDK DirectX 8。0
- DPIXELFORMAT
- 表面格式 WDK DirectX 8。0
- Fourcc
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e37b2ea7a98b0dc3530692eff08c87ba1245cb2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063446"
---
# <a name="surface-formats-as-fourccs"></a>将图面设为 FOURCC 格式


## <span id="ddk_surface_formats_as_fourccs_gg"></span><span id="DDK_SURFACE_FORMATS_AS_FOURCCS_GG"></span>


DirectX 8.0、D3DFMT Q8W8V8U8、D3DFMT V16U16 和 D3DFMT W11V11U10 定义的三个新的表面格式 \_ \_ \_ 将作为 *fourcc*传递给驱动程序。 这意味着， [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat) 数据结构的各个位深度和掩码字段未初始化且其值未定义。 因此，处理这三个格式的驱动程序不能依赖于像素格式的位计数或掩码，但必须根据需要进行计算。 例如，在计算这些类型之一的图面的螺距时，不得使用像素格式的 **dwRGBBitCount** 字段。 传递给驱动程序时，除 YUV、DXT 和 IHV 特定扩展格式以外的其他所有格式都将映射到旧的 DDPIXELFORMAT 表示形式，因此，在像素格式数据结构中具有有效的像素格式和掩码。

 

