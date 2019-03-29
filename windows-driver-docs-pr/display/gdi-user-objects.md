---
title: GDI 用户对象
description: GDI 用户对象
ms.assetid: 25048f14-a46e-49bb-8890-699bf1324007
keywords:
- GDI WDK Windows 2000 显示，用户对象
- 图形驱动程序 WDK Windows 2000 显示，用户对象
- 绘制 WDK GDI，用户对象
- 用户对象 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cbe8594a1691889c3595434e424f06f4c61e622e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576173"
---
# <a name="gdi-user-objects"></a>GDI 用户对象


## <span id="ddk_gdi_user_objects_gg"></span><span id="DDK_GDI_USER_OBJECTS_GG"></span>


GDI 维护内部数据结构，但通过将它们作为向下传递到这些结构的公共字段提供的驱动程序访问重要*用户对象*。 用户对象是 GDI 数据结构和驱动程序需要访问这些结构中的信息之间的接口的中间数据结构。 该驱动程序可以将指针传递给回 GDI 到查询的信息或寻求各种服务的用户对象。 与公共字段的用户对象提供以下优势：

-   它们不直接访问内部 GDI 数据结构相关的问题。

-   它们提供一个位置来保存驱动程序的 GDI 数据。 例如，PATHOBJ 结构可以包含要枚举与路径一样复杂对象所需的所有额外数据。

以下用户对象有：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff538261" data-raw-source="[&lt;strong&gt;BRUSHOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff538261)"><strong>BRUSHOBJ</strong></a></p></td>
<td align="left"><p>定义图形函数的输出行、 文本或填充的画笔对象。 驱动程序可以调用<a href="https://msdn.microsoft.com/library/windows/hardware/ff556272#wdkgloss-brushobj" data-raw-source="&lt;em&gt;BRUSHOBJ&lt;/em&gt;"> <em>BRUSHOBJ</em> </a>服务意识到画笔或查找以前缓存的通过 GDI 的实现。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff539417" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff539417)"><strong>CLIPOBJ</strong></a></p></td>
<td align="left"><p>该驱动程序提供访问权限<a href="https://msdn.microsoft.com/library/windows/hardware/ff556274#wdkgloss-clip-region" data-raw-source="&lt;em&gt;clip region&lt;/em&gt;"><em>剪辑区域</em></a>绘制或填充。 此区域可为一系列矩形的枚举。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565804" data-raw-source="[&lt;strong&gt;FLOATOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565804)"><strong>FLOATOBJ</strong></a></p></td>
<td align="left"><p>允许图形驱动程序来模拟浮点运算。 所有其他内核模式驱动程序将禁用浮点操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565974" data-raw-source="[&lt;strong&gt;FONTOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565974)"><strong>FONTOBJ</strong></a></p></td>
<td align="left"><p>使驱动程序访问有关特定实例 （或实现） 的一种字体的信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568844" data-raw-source="[&lt;strong&gt;PALOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568844)"><strong>PALOBJ</strong></a></p></td>
<td align="left"><p>一个包含 RGB 调色板颜色; 的结构可通过访问<a href="https://msdn.microsoft.com/library/windows/hardware/ff568845" data-raw-source="&lt;strong&gt;PALOBJ_cGetColors&lt;/strong&gt;"> <em>PALOBJ</em> </a>结构不包含任何公共成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff568849" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff568849)"><strong>PATHOBJ</strong></a></p></td>
<td align="left"><p>定义一个路径，指定将内容绘制 （行或贝塞尔曲线）。 一个<a href="https://msdn.microsoft.com/library/windows/hardware/ff556325#wdkgloss-pathobj" data-raw-source="&lt;em&gt;PATHOBJ&lt;/em&gt;"> <em>PATHOBJ</em> </a>结构传递给驱动程序来描述一组行和要对其应用笔划或填充的贝塞尔曲线。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569738" data-raw-source="[&lt;strong&gt;STROBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569738)"><strong>STROBJ</strong></a></p></td>
<td align="left"><p>枚举的驱动程序的标志符号句柄和描述要绘制的文本字符串的方式的位置的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff569901" data-raw-source="[&lt;strong&gt;SURFOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff569901)"><strong>SURFOBJ</strong></a></p></td>
<td align="left"><p>标识一个表面，这可以是 GDI 位图、 依赖于设备的位图或设备管理面。 请参阅<a href="surface-types.md" data-raw-source="[Surface Types](surface-types.md)">图面类型</a>有关详细信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570618" data-raw-source="[&lt;strong&gt;XFORMOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570618)"><strong>XFORMOBJ</strong></a></p></td>
<td align="left"><p>描述的任意线性二维转换，如几何宽线条。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff570634" data-raw-source="[&lt;strong&gt;XLATEOBJ&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff570634)"><strong>XLATEOBJ</strong></a></p></td>
<td align="left"><p>定义将像素从源图面格式转换为目标图面格式所需的翻译。</p></td>
</tr>
</tbody>
</table>

 

 

 





