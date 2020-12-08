---
title: 压缩纹理图面
description: 压缩纹理图面
keywords:
- 绘制压缩纹理 WDK DirectDraw，关于压缩纹理图面
- DirectDraw 压缩纹理 WDK Windows 2000 显示，关于压缩纹理图面
- 压缩纹理面 WDK DirectDraw，关于压缩纹理图面
- 表面 WDK DirectDraw，压缩纹理
- 纹理 WDK DirectDraw，压缩
- 绘制压缩纹理 WDK DirectDraw
- DirectDraw 压缩纹理 WDK Windows 2000 显示
- 压缩的纹理面 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d459215c0eac7a155c45e1c0cbd07f2141d8b81c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810215"
---
# <a name="compressed-texture-surfaces"></a>压缩纹理图面


## <span id="ddk_compressed_texture_surfaces_gg"></span><span id="DDK_COMPRESSED_TEXTURE_SURFACES_GG"></span>


图面可包含用于纹理3D 对象的位图。 为了减少纹理使用的内存量，Microsoft DirectDraw 支持纹理图面的压缩。

**注意**   尚未添加新的回调来支持压缩的纹理图面。 DirectDraw 通过现有的驱动程序回调将有关压缩纹理图面的信息传递给驱动程序。

 

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">FOURCC</th>
<th align="left">说明</th>
<th align="left">Alpha
<div>
 
</div>
预乘?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DXT1</p></td>
<td align="left"><p>不透明/一位 alpha</p></td>
<td align="left"><p>空值</p></td>
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
<td align="left"><p>内插 alpha</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DXT5</p></td>
<td align="left"><p>内插 alpha</p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

上面显示了驱动程序应支持的五种压缩纹理类型。

有关压缩纹理格式的详细信息，请参阅 DirectDraw SDK 文档中的 **压缩纹理格式** 。

 

 





