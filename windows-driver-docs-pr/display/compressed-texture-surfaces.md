---
title: 压缩纹理图面
description: 压缩纹理图面
ms.assetid: 72096a2a-5a4b-4800-bd99-6d403c54889d
keywords:
- 绘制压缩纹理 WDK DirectDraw 有关压缩的纹理图面
- 显示 DirectDraw 压缩纹理 WDK Windows 2000，关于压缩的纹理图面
- 有关压缩的纹理图面压缩的纹理图面 WDK DirectDraw
- WDK DirectDraw，压缩的纹理的图面
- 纹理 WDK DirectDraw 压缩
- 绘制压缩纹理 WDK DirectDraw
- DirectDraw 压缩纹理 WDK Windows 2000 显示
- 压缩的纹理的 WDK DirectDraw 图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 337c54f5856085967ce86b6b567369a881eba7d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362157"
---
# <a name="compressed-texture-surfaces"></a>压缩纹理图面


## <span id="ddk_compressed_texture_surfaces_gg"></span><span id="DDK_COMPRESSED_TEXTURE_SURFACES_GG"></span>


图面可以包含要用于纹理三维对象的位图。 若要减少的纹理占用的内存量，Microsoft DirectDraw 支持压缩的纹理图面。

**请注意**  添加了任何新的回调以支持压缩的纹理图面。 DirectDraw 将压缩的纹理图面有关的信息传递给驱动程序通过现有的驱动程序回调。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">FOURCC</th>
<th align="left">描述</th>
<th align="left">Alpha
<div>
 
</div>
自左乘？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXT1</p></td>
<td align="left"><p>不透明 / 一位 alpha</p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXT2</p></td>
<td align="left"><p>显式 alpha</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXT3</p></td>
<td align="left"><p>显式 alpha</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p>DXT4</p></td>
<td align="left"><p>内插的 alpha</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXT5</p></td>
<td align="left"><p>内插的 alpha</p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

在前面显示了五种类型的驱动程序应支持的压缩纹理。

有关压缩的纹理的格式的详细信息，请参阅**压缩纹理格式**DirectDraw SDK 文档中。

 

 





