---
title: 处理 DMA 样式 AGP
description: 处理 DMA 样式 AGP
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw，DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw，DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw，DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP、DMA 样式 AGP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 38329600ae5e06bf72befe22de48f61a736119db
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819121"
---
# <a name="handling-dma-style-agp"></a>处理 DMA 样式 AGP


## <span id="ddk_handling_dma_style_agp_gg"></span><span id="DDK_HANDLING_DMA_STYLE_AGP_GG"></span>


AGP 兼容的显示卡可以通过以下两种方式之一使用 AGP 内存：使用执行模型或直接内存访问 (DMA) 模型。

-   在执行模型中，如果非本地视频内存中有纹理，则该卡会直接访问 AGP 内存。 也就是说，如果卡是 AGP 内存中的纹理，它会直接从后备表面读取纹素数据， (系统内存副本) 的图面。

-   在 DMA 模型中，可以在执行纹理操作之前，将表面的内容显式移动到卡片上的本地显示内存。

需要特别注意的是，模型是指显示卡的客户端如何看到传输。 例如，当纹理时，显示卡可能会自动将纹素的数据从后备面移到小型本地显示内存缓存。 这似乎与 DMA 模型类似。 但是，由于客户端应用程序没有有关发生此传输的信息，因此显示卡实际上是公开执行模型。 仅当客户端应用程序必须采取明确的操作将后备图面的内容移到本地显示内存时，显示卡才被视为公开 DMA 模型。

前面几节介绍了 AGP 内存，其中介绍了驱动程序如何启用和公开 AGP 使用的执行模型。 本部分介绍了驱动程序必须执行的其他步骤才能向应用程序公开使用 DMA 模型 AGP。 请注意，驱动程序编写器必须决定是否在写入驱动程序时公开执行模型或 DMA 模型。 *驱动程序应公开一个模型，而不是同时公开两者。*

在从驱动程序公开 DMA 模型之前，请务必考虑将 DMA 模型对应用程序编写器的影响。 如果驱动程序公开执行模型 AGP 支持，则 DirectDraw 假定 AGP 中的表面 (非本地显示内存) ，本地显示内存在功能上相同。 因此，显示卡可以通过非本地或本地显示内存进行纹理操作，应用程序不需要执行任何其他操作。 设置呈现状态时，应用程序可以直接指定纹理图面的控点，而不管表面是在非本地还是在本地显示内存中。

但是，如果驱动程序公开 DMA 模型，则非本地显示内存中的表面可能与本地显示内存中的不同。 因此，在尝试从非本地显示内存图面的纹理之前，应用程序必须检查硬件是否能够从非本地显示内存中纹理。 这是通过检查驱动程序所公开的功能来实现的。 对于 blitting，情况也是如此。

应用程序通过 \_ 使用 DDSCAPS NONLOCALVIDMEM 指定 DDSCAPS VIDEOMEMORY 运算，显式请求 AGP 内存 \_ 。 如果应用程序未指定内存类型或仅指定 DDSCAPS \_ VIDEOMEMORY，则不考虑非本地显示内存。 此外，如果调用未指定本地或非本地显示内存，则图面为纹理，设备设置 D3DDEVCAPS \_ TEXTURENONLOCALVIDEOMEMORY 标志，然后可以在 AGP 内存中分配图面。

这意味着，如果驱动程序公开 DMA 模型，则不会从 AGP 内存中分配表面。 这与公开执行模型的驱动程序相反，其中，即使应用程序未显式请求 AGP 内存，也会分配 AGP 内存。 因此，公开执行模型的驱动程序更简单，使应用程序能够使用。 而且，执行模型驱动程序允许旧应用程序获得 AGP 的优势，而 DMA 模型驱动程序只会加速为 AGP 显式编写的新应用程序。 确定是要公开 execute 模型还是 DMA 模型时，应考虑此情况。

 

 





