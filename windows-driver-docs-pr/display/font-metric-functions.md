---
title: 字体规格函数
description: 字体规格函数
ms.assetid: 22d88765-bde5-4f1b-b106-9396868d6fb3
keywords:
- 字体 WDK 图形，指标函数
- GDI WDK Windows 2000 显示，字体，指标函数
- 图形驱动程序 WDK Windows 2000 显示，字体，指标功能
- DrvQueryFontData
- DrvQueryFontTree
- DrvFree
- DrvDestroyFont
- DrvQueryFont
- IFIMETRICS
- 光栅字体 WDK 图形
- 名义空间坐标系统 WDK 图形
- 调整 WDK 字体大小
- 度量值函数 WDK 字体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 242e58261cabc226dd2990173efa0a566875635a
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103602"
---
# <a name="font-metric-functions"></a>字体规格函数


## <span id="ddk_font_metric_functions_gg"></span><span id="DDK_FONT_METRIC_FUNCTIONS_GG"></span>


当驱动程序必须支持字体时，它必须通过 [**IFIMETRICS**](/windows/desktop/api/winddi/ns-winddi-_ifimetrics) 结构向 GDI 提供字体信息。 每个字体都有单独的 IFIMETRICS 结构。 大多数字段都以 FWORDs 表示，其中每个都有一个有符号的16位数量，位于设计空间。 如果字体是光栅字体，则设计空间和设备空间相同，字体单位相当于像素之间的距离。

基本上，IFIMETRICS 结构是文本度量结构的图形 DDI 版本。 所有距离都是指字体设计器的名义坐标系统。 "名义空间" 坐标系统是一个右笛卡尔坐标系统，其中 y 坐标增加到顶部，x 坐标向右增加。

IFIMETRICS 结构设计为具有可变长度。 对与字体关联的字符串的长度不施加限制。 常见的做法是在 IFIMETRICS 结构的最后一个字段之后存储字符串。

任何提供字体的驱动程序都必须支持 [**DrvQueryFont**](/windows/desktop/api/winddi/nf-winddi-drvqueryfont) 函数。 驱动程序还可以包括函数 [**DrvQueryFontData**](/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata) ，以检索有关已实现字体的信息。 在对 *DrvQueryFontData*的调用中，GDI 提供指向标志符号或字偶间距调整句柄的数组的指针。 驱动程序返回有关 GDI [**GLYPHDATA**](/windows/desktop/api/winddi/ns-winddi-_glyphdata) 结构中的关联标志符号的信息。 如果已为 *DrvQueryFontData* 提供字偶间距调整控点，则它将返回有关以 Win32 POINTL 结构形式提供的字偶间距调整的信息。 下表列出了字体指标函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvdestroyfont" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvdestroyfont)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>通知驱动程序不再需要字体实现，以便驱动程序可以释放它所分配的任何数据结构。 对于字体制造者，GDI 将调用此函数一次，对字体使用者调用一次。 可选-仅当驱动程序必须释放已分配的资源时才支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvfree" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvfree)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>通知驱动程序不再需要指示的数据结构。 可选-仅当驱动程序的内存管理需要此信息时才应实现。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvqueryfont" data-raw-source="[&lt;strong&gt;DrvQueryFont&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfont)"><strong>DrvQueryFont</strong></a></p></td>
<td align="left"><p>返回一个指向字体的 <a href="/windows/desktop/api/winddi/ns-winddi-_ifimetrics" data-raw-source="[&lt;strong&gt;IFIMETRICS&lt;/strong&gt;](/windows/desktop/api/winddi/ns-winddi-_ifimetrics)"><strong>IFIMETRICS</strong></a> 结构的指针。 处理字体的所有驱动程序所必需的。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata" data-raw-source="[&lt;strong&gt;DrvQueryFontData&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfontdata)"><strong>DrvQueryFontData</strong></a></p></td>
<td align="left"><p>返回有关已实现字体的信息。 需要 (用于处理字体的所有驱动程序) 所选的 <em>iMode</em> 值。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/desktop/api/winddi/nf-winddi-drvqueryfonttree" data-raw-source="[&lt;strong&gt;DrvQueryFontTree&lt;/strong&gt;](/windows/desktop/api/winddi/nf-winddi-drvqueryfonttree)"><strong>DrvQueryFontTree</strong></a></p></td>
<td align="left"><p>返回指向结构的指针，这些结构定义从 Unicode 到标志符号句柄的映射或字偶间距对到字偶间距调整句柄的映射。 处理字体的所有驱动程序所必需的。</p></td>
</tr>
</tbody>
</table>

 

函数 *DrvQueryFontTree* 允许 GDI 获取树结构的指针，这些结构定义以下内容之一：

-   从 Unicode 映射到标志符号句柄，包括 (GDI [**FD \_ GLYPHSET**](/windows/desktop/api/winddi/ns-winddi-_fd_glyphset) 结构的字形变体) 

-   将字偶间距调整对映射到字偶间距调整图柄 ([**FD \_ KERNINGPAIR**](/windows/desktop/api/winddi/ns-winddi-_fd_kerningpair) 结构) 

*DrvQueryFontTree* 需要努力才能生成所需的结构，因此，如果可能，驱动程序应预先计算这些文件。 结构可以存储在资源中，也可以存储在文件中。 如果结构存储在文件中，则加载或读取它们的理想方法是调用 [**EngMapFontFile**](/windows/desktop/api/winddi/nf-winddi-engmapfontfile) 函数，该函数将文件映射到内存。 由于文件未添加到交换文件中，因此，如果需要，可以使用内存，这比在文件中打开和读取更有效。

具体而言，驱动程序将在 *pid* 参数中返回标识符。 当不再需要[**fd \_ GLYPHSET**](/windows/desktop/api/winddi/ns-winddi-_fd_glyphset)结构或[**fd \_ KERNINGPAIR**](/windows/desktop/api/winddi/ns-winddi-_fd_kerningpair)结构数组时，GDI 会将其传递到[**DrvFree**](/windows/desktop/api/winddi/nf-winddi-drvfree)函数，并返回指针。 根据驱动程序中管理内存的方式， *pid* 可以标识结构，确定结构的分配方式，或者根本不执行任何操作。

[**DrvFree**](/windows/desktop/api/winddi/nf-winddi-drvfree) 和 [**DrvDestroyFont**](/windows/desktop/api/winddi/nf-winddi-drvdestroyfont) 都是可选函数。 GDI 调用 *DrvFree* 来通知驱动程序，不再需要指定的数据结构。 该驱动程序无需实现它，除非它为结构分配内存，并且在可释放相应的数据结构时需要通知。 例如，如果数据与 [**FONTOBJ**](/windows/desktop/api/winddi/ns-winddi-_fontobj) 结构相关联，则删除可能会推迟到对 *DrvDestroyFont*的调用，因此不需要实现 *DrvFree*。

*DrvDestroyFont* 通知驱动程序不再需要字体实现，以便驱动程序可以释放它所分配的任何数据结构。 对于字体制造者，GDI 将调用此函数一次，对字体使用者调用一次。 仅当该字体实例被销毁时，驱动程序必须释放已分配的资源。

