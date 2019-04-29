---
title: 4 2 0 视频的像素格式
description: 4 2 0 视频的像素格式
ms.assetid: fb83336b-ff71-4f54-b833-324da60e7f9e
keywords:
- 未压缩视频的像素格式 WDK DirectX VA
- 未压缩的视频 WDK DirectX VA 的像素格式
- 解码 WDK DirectX va，因此未压缩的视频的像素格式的压缩的图片
- 图片解码 WDK DirectX VA，压缩
- 4 2 0 视频 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b4de7df17be95da7aa3f4efcd5d757ab4b00359
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391256"
---
# <a name="420-video-pixel-formats"></a>4:2:0 视频像素格式


## <span id="ddk_4_2_0_video_pixel_formats_gg"></span><span id="DDK_4_2_0_VIDEO_PIXEL_FORMATS_GG"></span>


要解码压缩的 4:2:0 视频，请使用其中一个的以下未压缩的像素格式。

| **像素格式** | **说明** | 
|:--|:--|
| YUY2 | 如中所述[4:2:2 视频像素格式](vscode-resource://c:/drivers/drivers/windows-driver-docs-pr/display/4-2-2-video-pixel-formats.md)，不同之处在于两个行的输出 Cb 和 Cr 示例生成每个实际行，共 4 步： 2:0 Cb 和 Cr 示例。 每个对输出行的第二行是通常在第一行的重复或求平均值对的第一行中的第一个行的下一步对示例的示例生成。 | 
| UYVY | 如中所述[4:2:2 视频像素格式](vscode-resource://c:/drivers/drivers/windows-driver-docs-pr/display/4-2-2-video-pixel-formats.md)，不同之处在于两个行的输出 Cb 和 Cr 示例生成每个实际行，共 4 步： 2:0 Cb 和 Cr 示例。 每个对输出行的第二行是通常在第一行的重复或求平均值对的第一行中的第一个行的下一步对示例的示例生成。 | 
| YV12 | Y 的所有示例都是在内存中首次发现作为数组的无符号 char （可能具有更大的步幅内存对齐方式），后面紧随所有 Cr 示例 （带一半的步幅 Y 线条和一半数目的行），则都紧跟所有 Cb以类似的方式的示例。 | 
| IYUV | 与 YV12，除了交换 Cb 和 Cr 平面的顺序相同。 | 
| NV12 | 一种格式中的所有 Y 找到示例首先在内存中为无符号 char 数组具有偶数数目的行 （也许加上内存对齐方式的更大跨距）。 这被紧跟包含交错的 Cb 和 Cr 示例的无符号 char 类型的数组。 如果这些示例都作为小字节序 WORD 类型，Cb 是以最低有效位为单位，Cr 将是在使用相同的总 stride 作为 Y 示例的最高有效位。 NV12 为首选的 4:2:0 像素格式。 | 
| NV21 | NV12，除非该 Cb 和 Cr 示例相同，以便无符号 char 色度数组必须跟 Cb 为每个示例 （以便以小字节序 WORD 类型寻址，如果 Cr 将能够以最低有效位为单位，并 Cb 会采用最登录 Cr 交换ificant 位）。 | 
| IMC1 | YV12，相同，只不过 Cb 和 Cr 的步幅平面等同于 Y 平面的跨距。 此外，Cb 和 Cr 平面必须位于在 16 行的多个内存边界上。 下面的代码示例显示为 Cb 的计算和 Cr 平面。<br/>`BYTE* pCr = pY + (((Height + 15) & ~15) * Stride);`<br/>`BYTE* pCb = pY + (((((Height * 3) / 2) + 15) & ~15) * Stride);`<br/>在上述示例中上, 一年度是一个字节的指针，指向内存数组的开头和高度必须是 16 的倍数。 | 
| IMC2 | 在后半部分 stride 边界交错 IMC1，除非该 Cb 和 Cr 行相同。 换而言之，色度区域中的每个完整 stride 行开头 Cr，跟 Cb 在下一步的后半部分 stride 边界处开始的行的行。 （这是更多地址空间-高效格式比 IMC1，因为它会减少了一半，色度地址空间，并因此降低总地址空间的 25%。）这是相对于 NV12，可以选择首选的格式，但 NV12 似乎更受欢迎。 | 
| IMC3 | 与 IMC1，除了交换 Cb 和 Cr 相同。 | 
| IMC4 | 与 IMC2，除了交换 Cb 和 Cr 相同。 | 

有关这些格式的详细信息，请参阅[建议的 8 位 YUV 格式的视频呈现](https://msdn.microsoft.com/library/windows/desktop/dd206750)Microsoft Media Foundation 文档中。
