---
title: 4 2 2 视频的像素格式
description: 4 2 2 视频的像素格式
ms.assetid: 7064c7bd-bc7d-4b71-8876-ccb3a5808e45
keywords:
- 未压缩视频的像素格式 WDK DirectX VA
- 未压缩的视频 WDK DirectX VA 的像素格式
- 解码 WDK DirectX va，因此未压缩的视频的像素格式的压缩的图片
- 图片解码 WDK DirectX VA，压缩
- 4 2 2 视频 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0919efd2985e1c6dbb449267ce32f39943036c54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542796"
---
# <a name="422-video-pixel-formats"></a>4:2:2 视频的像素格式


## <span id="ddk_4_2_2_video_pixel_formats_gg"></span><span id="DDK_4_2_2_VIDEO_PIXEL_FORMATS_GG"></span>


要解码压缩的 4:2:2 视频，请使用其中一个的以下未压缩的像素格式。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">像素格式</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>YUY2</p></td>
<td align="left"><p>作为数组中的第一个字节包含 Y 的第一个示例的无符号字符在内存中找到数据、 第二个字节包含 Cb 第一个示例中，第三个字节包含 Y 的第二个示例、 第四个字节包含 Cr; 第一个示例等等。 如果两个小字节序 WORD 类型变量的形式处理的数据，第一个单词中最高有效位，在最低有效位和 Cb 包含 Y₀ 和第二个字中的最高有效位最低有效位和 Cr 中包含 Y₁。 YUY2 是首选的 DirectX VA 4:2:2 的像素格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UYVY</p></td>
<td align="left"><p>与 YUY2，除了交换中的每个单词的字节顺序相同。 如果两个小字节序 WORD 类型变量的形式处理的数据，第一个单词中最高有效位，在最低有效位和 Y₀ 包含 Cb 和第二个字中的最高有效位最低有效位和 Y₁ 中包含 Cr。</p></td>
</tr>
</tbody>
</table>

 

 

 





