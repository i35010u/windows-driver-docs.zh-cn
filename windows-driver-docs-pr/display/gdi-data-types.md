---
title: GDI 数据类型
description: GDI 数据类型
keywords:
- GDI WDK Windows 2000 显示，数据类型
- 图形驱动程序 WDK Windows 2000 显示，数据类型
- 绘制 WDK GDI，数据类型
- 数据类型 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b863e32d33ee240c91be8c582b49b5029fb0159a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821561"
---
# <a name="gdi-data-types"></a>GDI 数据类型


## <span id="ddk_gdi_data_types_gg"></span><span id="DDK_GDI_DATA_TYPES_GG"></span>


在下表中定义的数据类型将出现在设备驱动程序界面中。 [GDI 用户对象](gdi-user-objects.md)中已经介绍了几个列出的数据类型。 作为指针的数据类型用星号标记 (\*) 。

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
<td align="left"><p>一个可为 <strong>TRUE</strong> 或 <strong>FALSE</strong>的32位值。</p></td>
</tr>
<tr class="even">
<td align="left"><p>BYTE</p></td>
<td align="left"><p>j</p></td>
<td align="left"><p>8 位无符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>BRUSHOBJ<em></p></td>
<td align="left"><p>pbo</p></td>
<td align="left"><p>指向画笔对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>CLIPLINE</p></td>
<td align="left"><p>cl</p></td>
<td align="left"><p>一个 clipline 对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>CLIPOBJ</em></p></td>
<td align="left"><p>pco</p></td>
<td align="left"><p>指向剪辑对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DHPDEV</p></td>
<td align="left"><p>dhpdev</p></td>
<td align="left"><p>由设备驱动程序定义的、用于标识物理设备的32位句柄。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DHSURF</p></td>
<td align="left"><p>dhsurf</p></td>
<td align="left"><p>由设备驱动程序定义的32位句柄，用于标识设备管理的图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FIX</p></td>
<td align="left"><p>修复</p></td>
<td align="left"><p>固定点数字。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLOATL</p></td>
<td align="left"><p>E</p></td>
<td align="left"><p>一个浮点数字。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FLOAT_LONG</p></td>
<td align="left"><p>el</p></td>
<td align="left"><p>将解释为 LONG 或 FLOATL 的32位重载值，具体取决于上下文。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FLONG</p></td>
<td align="left"><p>fl</p></td>
<td align="left"><p>一组32位标志。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FONTOBJ<em></p></td>
<td align="left"><p>pfo</p></td>
<td align="left"><p>指向字体对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FSHORT</p></td>
<td align="left"><p>fs</p></td>
<td align="left"><p>一组16位标志。</p></td>
</tr>
<tr class="even">
<td align="left"><p>FWORD</p></td>
<td align="left"><p>转发</p></td>
<td align="left"><p>16 位带符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HBM</p></td>
<td align="left"><p>hbm</p></td>
<td align="left"><p>由 GDI 定义的32位句柄，用于标识位图。</p></td>
</tr>
<tr class="even">
<td align="left"><p>HPAL</p></td>
<td align="left"><p>hpal</p></td>
<td align="left"><p>由 GDI 定义的32位句柄，用于标识调色板。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>HSURF</p></td>
<td align="left"><p>hsurf</p></td>
<td align="left"><p>由 GDI 定义的32位句柄，用于标识图面。</p></td>
</tr>
<tr class="even">
<td align="left"><p>LONG</p></td>
<td align="left"><p>l</p></td>
<td align="left"><p>32 位带符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>组合</p></td>
<td align="left"><p>组合</p></td>
<td align="left"><p>32位的数量，其低16位定义前台和后台组合模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PALOBJ</em></p></td>
<td align="left"><p>ppalo</p></td>
<td align="left"><p>指向调色板对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PATHOBJ<em></p></td>
<td align="left"><p>ppo</p></td>
<td align="left"><p>指向路径对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>POINTE</p></td>
<td align="left"><p>pte</p></td>
<td align="left"><p>包含 {FLOATL <strong>x</strong>， <strong>y</strong>;} 的点结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>POINTFIX</p></td>
<td align="left"><p>ptfx</p></td>
<td align="left"><p>包含 {FIX <strong>x</strong>， <strong>y</strong>;} 的点结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>POINTQF</p></td>
<td align="left"><p>ptq</p></td>
<td align="left"><p>包含 {LARGE_INTEGER <strong>x</strong>， <strong>y</strong>;} 的点结构。 此结构的每个成员都是28.36 格式的64位坐标。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>PWSZ</p></td>
<td align="left"><p>pwsz</p></td>
<td align="left"><p>指向以 null 结尾的 Unicode 字符串的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>PVOID</p></td>
<td align="left"><p>pv</p></td>
<td align="left"><p>指向 VOID 的指针，该类型是未定义的数据类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>RECTFX</p></td>
<td align="left"><p>rcfx</p></td>
<td align="left"><p>由 {FIX <strong>xLeft</strong>， <strong>yTop</strong>， <strong>xRight</strong>， <strong>yBottom</strong>;} 组成的矩形结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ROP4</p></td>
<td align="left"><p>rop4</p></td>
<td align="left"><p>一个32位值，指定如何混合源、目标、模式和掩码像素。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SHORT</p></td>
<td align="left"><p>s</p></td>
<td align="left"><p>16 位带符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SIZEL</p></td>
<td align="left"><p>sizl</p></td>
<td align="left"><p>一个结构，其中包含 {LONG <strong>cx</strong>， <strong>cy</strong>;}。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STROBJ</em></p></td>
<td align="left"><p>pstro</p></td>
<td align="left"><p>指向文本字符串对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SURFOBJ<em></p></td>
<td align="left"><p>pso</p></td>
<td align="left"><p>指向 surface 对象的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ULONG</p></td>
<td align="left"><p>ul</p></td>
<td align="left"><p>32 位无符号整数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>USHORT</p></td>
<td align="left"><p>us</p></td>
<td align="left"><p>16 位无符号整数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>XFORMOBJ</em></p></td>
<td align="left"><p>pxo</p></td>
<td align="left"><p>指向坐标转换对象的指针。</p></td>
</tr>
<tr class="even">
<td align="left"><p>XLATEOBJ*</p></td>
<td align="left"><p>pxlo</p></td>
<td align="left"><p>指向颜色转换对象的指针。</p></td>
</tr>
</tbody>
</table>

 

下表中列出的参数前缀用于根据变量的用法修改变量名称前缀。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">前缀</th>
<th align="left">参数用法</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>i</p></td>
<td align="left"><p>枚举索引</p></td>
</tr>
<tr class="even">
<td align="left"><p>c</p></td>
<td align="left"><p>计数</p></td>
</tr>
<tr class="odd">
<td align="left"><p>p</p></td>
<td align="left"><p>一个指针</p></td>
</tr>
</tbody>
</table>

 

 

 





