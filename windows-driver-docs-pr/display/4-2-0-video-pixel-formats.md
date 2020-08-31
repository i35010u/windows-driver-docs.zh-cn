---
title: 4 2 0 视频像素格式
description: 4 2 0 视频像素格式
ms.assetid: fb83336b-ff71-4f54-b833-324da60e7f9e
keywords:
- 未压缩的视频像素格式 WDK DirectX VA
- 未压缩的视频 WDK DirectX VA 的像素格式
- 压缩的图片解码 WDK DirectX VA，未压缩视频的像素格式
- 图片解码 WDK DirectX VA，已压缩
- 4 2 0 视频 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40a331c34a7e87f758e315d9435a8119b8e060ce
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064412"
---
# <a name="420-video-pixel-formats"></a>4:2:0 视频像素格式

## <span id="ddk_4_2_0_video_pixel_formats_gg"></span><span id="DDK_4_2_0_VIDEO_PIXEL_FORMATS_GG"></span>

若要解码压缩的4:2:0 视频，请使用以下未压缩的像素格式之一。

| 像素格式 | 说明 |
| ------------ | ----------- |
| YUY2 | 如 [4:2:2 视频像素格式](4-2-2-video-pixel-formats.md)中所述，例外情况除外，只为每个实际 4:2:0 Cb 和 cr 示例行生成两行输出 Cb 和 cr 示例。 每对输出行中的第二行通常是第一行的副本，或使用下一对的第一行的样本对第一行中的样本求平均值来生成。 |
| UYVY | 如 [4:2:2 视频像素格式](4-2-2-video-pixel-formats.md)中所述，例外情况除外，只为每个实际 4:2:0 Cb 和 cr 示例行生成两行输出 Cb 和 cr 示例。 每对输出行中的第二行通常是第一行的副本，或使用下一对的第一行的样本对第一行中的样本求平均值来生成。 |
| YV12 | 所有 Y 样本都首先在内存中作为一个无符号 char 数组提供 (可能具有更大的内存对齐方式) ，后面紧跟所有 Cr 示例 (，其中一半的行跨距为一半，最后是) 的行数的一半，然后按照类似的方式在所有 Cb 示例的后面紧跟。 |
| IYUV | 与 YV12 相同，不同之处在于交换 Cb 和 Cr 平面的顺序。 |
| NV12 | 一种格式，其中，在内存中首先找到所有 Y 样本，其中包含偶数行的无符号 char 数组 (可能具有更大的内存对齐) 跨距。 紧跟在包含交错的 Cb 和 Cr 示例的无符号 char 数组之后。 如果将这些示例作为小 endian 字类型进行寻址，则 Cb 将处于最小有效位，而 Cr 与 Y 样本具有相同的总步幅。 NV12 是首选的4:2:0 像素格式。 |
| NV21 | 与 NV12 相同，不同之处在于，已交换 Cb 和 Cr 示例，使无符号 char 的色度数组对于每个示例都具有 Cr 后跟 Cb (例如，如果作为小字节序 WORD 类型处理，Cr 将处于最小有效位，并且 Cb 应为最有效的位) 。 |
| IMC1 | 与 YV12 相同，不同之处在于 Cb 和 Cr 平面的跨距与 Y 平面中的跨距相同。 此外，Cb 和 Cr 平面必须位于16行的倍数的内存边界上。 下面的代码示例显示了 Cb 和 Cr 平面的计算。<br/>`BYTE* pCr = pY + (((Height + 15) & ~15) * Stride);`<br/>`BYTE* pCb = pY + (((((Height * 3) / 2) + 15) & ~15) * Stride);`<br/>在前面的示例中，pY 是一个字节指针，指向内存数组的开头，高度必须是16的倍数。 |
| IMC2 | 与 IMC1 相同，只不过 Cb 和 Cr 行以半步幅边界交错。 换句话说，色度区域中的每个全步幅行将以 Cr 开头，后跟一个从下半个跨距边界开始的 Cb 行。  (这是一个比 IMC1 更多的地址空间高效格式，因为它将色度的地址空间剪切为一半，从而将总地址空间按25% 剪切。 ) 这是与 NV12 相关的首选格式，但 NV12 似乎更受欢迎。 |
| IMC3 | 与 IMC1 相同，但交换 Cb 和 Cr 除外。 |
| IMC4 | 与 IMC2 相同，但交换 Cb 和 Cr 除外。 |

有关这些格式的详细信息，请参阅 Microsoft 媒体基础文档中 [的视频呈现的建议8位 YUV 格式](/windows/desktop/medfound/recommended-8-bit-yuv-formats-for-video-rendering) 。