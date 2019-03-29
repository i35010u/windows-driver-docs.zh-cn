---
title: 处理 DMA 样式 AGP
description: 处理 DMA 样式 AGP
ms.assetid: f43f662f-0036-4725-ad6b-5b836b23a734
keywords:
- DMA 样式 AGP WDK DirectDraw
- 显示内存 WDK DirectDraw DMA 样式 AGP
- 非本地显示内存 WDK DirectDraw DMA 样式 AGP
- AGP WDK DirectDraw，DMA 样式 AGP
- 绘制 AGP 支持 WDK DirectDraw DMA 样式 AGP
- DirectDraw AGP 支持 WDK Windows 2000 显示，DMA 样式 AGP
- 内存 WDK DirectDraw AGP DMA 样式 AGP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce2829665656167a0fcd2cd84f32eeb7e7ad67d9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562138"
---
# <a name="handling-dma-style-agp"></a>处理 DMA 样式 AGP


## <span id="ddk_handling_dma_style_agp_gg"></span><span id="DDK_HANDLING_DMA_STYLE_AGP_GG"></span>


AGP 兼容显示卡可以在两种方式之一使用 AGP 内存： 使用执行模型或直接内存访问 (DMA) 模型。

-   在执行模型中，如果在非本地视频内存中，纹理卡 AGP 内存直接访问。 即，数据卡设置从 AGP 内存它直接从后备面 （系统内存复制的图面） 读取纹素数据。

-   在 DMA 模型中，应用层协议内容必须显式移动到本地显示内存卡上才可以执行纹理绘制操作。

请务必注意，该模型是指如何显示卡的客户端看到传输。 例如，显示卡可能会自动将纹素数据从后备面到小型本地显示内存缓存纹理时。 这可能看起来好像 DMA 模型。 但是，由于客户端应用程序没有有关发生此传输的信息，显示卡，事实上，公开了一个执行模型。 仅当客户端应用程序必须获得明确的操作将备份图面的内容移动到本地显示内存时，才显示卡视为公开 DMA 模型。

处理的 AGP 内存前面几节介绍了如何启用和公开 AGP 使用情况的执行模型驱动程序。 本部分介绍驱动程序来公开 DMA 模型 AGP 到应用程序的使用而必须执行其他步骤。 请注意，驱动程序编写器必须决定是否公开 execute 模型或 DMA 模型编写驱动程序时。 *该驱动程序应公开一个模型或另一个，但不可同时使用两者。*

在之前公开某个驱动程序的 DMA 模型，务必要考虑到应用程序编写器的 DMA 模型的含义。 如果驱动程序将公开执行模型 AGP 支持、 DirectDraw 假定 AGP （非本地显示内存） 和本地显示内存中的图面是功能上相同。 因此显示卡可以纹理由应用程序从非本地或本地的显示内存而无需任何其他操作。 在设置时的呈现状态，应用程序可以指定的句柄纹理图面直接，而不管在图面是在非本地或本地的显示内存中。

但是，如果驱动程序公开 DMA 模型，在非本地显示内存中的图面可能具有不同的功能，与在本地显示内存中。 因此，再尝试纹理从非本地显示内存图面，该应用程序必须检查硬件是否能够从非本地显示内存的纹理。 这被实现通过检查由驱动程序公开的功能。 同样适用于平面闪。

应用程序显式请求 AGP 内存通过指定 DDSCAPS\_与 DDSCAPS 的 VIDEOMEMORY 或运算\_NONLOCALVIDMEM。 如果应用程序未指定内存类型或仅指定 DDSCAPS\_VIDEOMEMORY，不考虑非本地显示内存。 此外，如果调用未指定本地或非本地显示内存，在图面是一种纹理，并在设备设置 D3DDEVCAPS\_可以在 AGP 内存中分配 TEXTURENONLOCALVIDEOMEMORY 标志，然后在图面。

这意味着，如果驱动程序公开 DMA 模型，表面不分配给从 AGP 内存。 这与驱动程序公开执行的模型，即使应用程序不会显式请求它的 AGP 中分配内存。 因此，公开执行模型的驱动程序是要简单得多的应用程序使用。 此外，执行模型驱动程序允许旧应用程序能够受益于 AGP，而 DMA 模型驱动程序仅加速为 AGP 显式编写的新应用程序。 在决定是否要公开 execute 或 DMA 模型时应将此视为。

 

 





