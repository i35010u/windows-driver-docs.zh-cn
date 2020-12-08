---
title: 4 2 2 视频像素格式
description: 4 2 2 视频像素格式
keywords:
- 未压缩的视频像素格式 WDK DirectX VA
- 未压缩的视频 WDK DirectX VA 的像素格式
- 压缩的图片解码 WDK DirectX VA，未压缩视频的像素格式
- 图片解码 WDK DirectX VA，已压缩
- 4 2 2 视频 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d59be9de1a31ed53f990bbbcda9d334a214a9807
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810587"
---
# <a name="422-video-pixel-formats"></a>4:2:2 视频像素格式


## <span id="ddk_4_2_2_video_pixel_formats_gg"></span><span id="DDK_4_2_2_VIDEO_PIXEL_FORMATS_GG"></span>


若要解码压缩的4:2:2 视频，请使用以下未压缩的像素格式之一。

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
<td align="left"><p>数据以无符号字符数组的形式出现在内存中，其中第一个字节包含第一个第一个示例，第二个字节包含第一个第一个示例，第三个字节包含第一个第一个示例，第四个字节包含 Cr 的第一个样本;依此类推。 如果将数据作为两个小字节序 WORD 类型变量的数组进行寻址，则第一个词将在最高有效位中包含 Y ₀，在最高有效位中包含 Cb，第二个单词在最高有效位中包含 Y ₁，在最高有效位中包含 Cr。 YUY2 是首选的 DirectX VA 4:2:2 像素格式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>UYVY</p></td>
<td align="left"><p>与 YUY2 相同，不同之处在于交换每个单词中的字节顺序。 如果将数据作为两个小字节序 WORD 类型变量的数组进行寻址，则第一个词将在最高有效位中包含 Cb，在最高有效位中包含 Y ₀，第二个单词在最高有效位中包含 Cr，在最高有效位中包含 Y ₁。</p></td>
</tr>
</tbody>
</table>

 

 

 





