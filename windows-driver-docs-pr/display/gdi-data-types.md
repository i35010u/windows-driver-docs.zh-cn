---
title: GDI 数据类型
description: GDI 数据类型
ms.assetid: 2054aa16-6d86-4db3-8b16-4570b0374e23
keywords:
- GDI WDK Windows 2000 显示中，数据类型
- 图形驱动程序 WDK Windows 2000 显示中，数据类型
- 绘制 WDK GDI，数据类型
- 数据类型 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c4fa605d9bbd5974a142e4175ff4454e1007a78
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63385029"
---
# <a name="gdi-data-types"></a>GDI 数据类型


## <span id="ddk_gdi_data_types_gg"></span><span id="DDK_GDI_DATA_TYPES_GG"></span>


下表中定义的数据类型显示在设备驱动程序接口。 多个列出的数据类型已描述中[GDI 用户对象](gdi-user-objects.md)。 是指针的数据类型将标有星号 (\*)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">图形 DDI 数据类型</th>
<th align="left">变量名称前缀</th>
<th align="left">定义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>BOOL</p></td>
<td align="left"><p>b</p></td>
<td align="left"><p>可以是一个 32 位值<strong>，则返回 TRUE</strong>或<strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BYTE</p></td>
<td align="left"><p>j</p></td>
<td align="left"><p>一个 8 位无符号的整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRUSHOBJ<em></p></td>
<td align="left"><p>pbo</p></td>
<td align="left"><p>指向一个画笔对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CLIPLINE</p></td>
<td align="left"><p>cl</p></td>
<td align="left"><p>一个 clipline 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLIPOBJ</em></p></td>
<td align="left"><p>pco</p></td>
<td align="left"><p>指向一个剪辑对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DHPDEV</p></td>
<td align="left"><p>dhpdev</p></td>
<td align="left"><p>由设备驱动程序，用于标识物理设备定义一个 32 位句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DHSURF</p></td>
<td align="left"><p>dhsurf</p></td>
<td align="left"><p>由设备驱动程序，用于标识设备管理面定义一个 32 位句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FIX</p></td>
<td align="left"><p>修复</p></td>
<td align="left"><p>固定点数字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLOATL</p></td>
<td align="left"><p>E</p></td>
<td align="left"><p>一个浮点数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLOAT_LONG</p></td>
<td align="left"><p>el</p></td>
<td align="left"><p>一个 32 位重载值，该值被解释为 long 类型的值或 FLOATL，具体取决于上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLONG</p></td>
<td align="left"><p>fl</p></td>
<td align="left"><p>32 位标志的一组。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FONTOBJ<em></p></td>
<td align="left"><p>pfo</p></td>
<td align="left"><p>指向字体对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSHORT</p></td>
<td align="left"><p>fs</p></td>
<td align="left"><p>一组 16 位标志。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FWORD</p></td>
<td align="left"><p>fw</p></td>
<td align="left"><p>一个 16 位有符号的整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBM</p></td>
<td align="left"><p>hbm</p></td>
<td align="left"><p>通过 GDI，用于标识位图定义一个 32 位句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HPAL</p></td>
<td align="left"><p>hpal</p></td>
<td align="left"><p>通过 GDI，标识调色板定义一个 32 位句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HSURF</p></td>
<td align="left"><p>hsurf</p></td>
<td align="left"><p>通过 GDI，标识一个面定义一个 32 位句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p>长</p></td>
<td align="left"><p>l</p></td>
<td align="left"><p>一个 32 位有符号的整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>MIX</p></td>
<td align="left"><p>mix</p></td>
<td align="left"><p>32 位数量，其低 16 位定义前景色和背景混合模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PALOBJ</em></p></td>
<td align="left"><p>ppalo</p></td>
<td align="left"><p>指向调色板对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PATHOBJ<em></p></td>
<td align="left"><p>ppo</p></td>
<td align="left"><p>指向一个路径对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>POINTE</p></td>
<td align="left"><p>pte</p></td>
<td align="left"><p>组成的点结构 {FLOATL <strong>x</strong>， <strong>y</strong>;}。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>POINTFIX</p></td>
<td align="left"><p>ptfx</p></td>
<td align="left"><p>组成的点结构 {修复<strong>x</strong>， <strong>y</strong>;}。</p></td>
</tr>
<tr class="even">
<td align="left"><p>POINTQF</p></td>
<td align="left"><p>ptq</p></td>
<td align="left"><p>组成的点结构 {LARGE_INTEGER <strong>x</strong>， <strong>y</strong>;}。 此结构的每个成员是 28.36 格式的 64 位坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PWSZ</p></td>
<td align="left"><p>pwsz</p></td>
<td align="left"><p>指向以 null 结尾的 Unicode 字符串的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PVOID</p></td>
<td align="left"><p>pv</p></td>
<td align="left"><p>指向 VOID、 未定义的数据类型的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RECTFX</p></td>
<td align="left"><p>rcfx</p></td>
<td align="left"><p>包含一个矩形结构 {修复<strong>xLeft</strong>，<strong>由</strong>， <strong>xRight</strong>， <strong>yBottom</strong>;}。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROP4</p></td>
<td align="left"><p>rop4</p></td>
<td align="left"><p>一个 32 位值，该值指定源、 目标、 模式和掩码像素的方式混合使用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>短</p></td>
<td align="left"><p>文件</p></td>
<td align="left"><p>一个 16 位有符号的整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>为原始大小</p></td>
<td align="left"><p>sizl</p></td>
<td align="left"><p>组成的结构 {长<strong>cx</strong>， <strong>cy</strong>;}。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STROBJ</em></p></td>
<td align="left"><p>pstro</p></td>
<td align="left"><p>指向一个文本字符串对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SURFOBJ<em></p></td>
<td align="left"><p>pso</p></td>
<td align="left"><p>指向图面上对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ULONG</p></td>
<td align="left"><p>ul</p></td>
<td align="left"><p>一个 32 位无符号的整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT</p></td>
<td align="left"><p>us</p></td>
<td align="left"><p>一个 16 位无符号的整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XFORMOBJ</em></p></td>
<td align="left"><p>pxo</p></td>
<td align="left"><p>指向坐标转换对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>XLATEOBJ*</p></td>
<td align="left"><p>pxlo</p></td>
<td align="left"><p>指向一个颜色转换对象的指针。</p></td>
</tr>
</tbody>
</table>

 

下表中列出的参数前缀用于修改根据其使用情况的变量名称前缀。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">前缀</th>
<th align="left">参数的用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>图标</p></td>
<td align="left"><p>枚举的索引</p></td>
</tr>
<tr class="even">
<td align="left"><p>c</p></td>
<td align="left"><p>计数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>p</p></td>
<td align="left"><p>一个指针，</p></td>
</tr>
</tbody>
</table>

 

 

 





