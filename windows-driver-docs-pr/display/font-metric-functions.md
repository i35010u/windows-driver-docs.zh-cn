---
title: 字体规格函数
description: 字体规格函数
ms.assetid: 22d88765-bde5-4f1b-b106-9396868d6fb3
keywords:
- 字体 WDK 图形，指标函数
- GDI WDK Windows 2000 显示、 字体、 度量值的函数
- 图形驱动程序 WDK Windows 2000 显示，字体，指标函数
- DrvQueryFontData
- DrvQueryFontTree
- DrvFree
- DrvDestroyFont
- DrvQueryFont
- IFIMETRICS
- 光栅字体 WDK 图形
- 名义空间坐标系统 WDK 图形
- 大小 WDK 字体
- 指标函数 WDK 字体
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 87a5e4126a6c68ab80380393f252eba74dbc6a5e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338637"
---
# <a name="font-metric-functions"></a>字体规格函数


## <span id="ddk_font_metric_functions_gg"></span><span id="DDK_FONT_METRIC_FUNCTIONS_GG"></span>


如果驱动程序必须支持字体，它必须提供字体信息向通过 GDI [ **IFIMETRICS** ](https://msdn.microsoft.com/library/windows/hardware/ff567418)结构。 没有单独的 IFIMETRICS 结构的每种字体。 大多数字段以 FWORDs，表示每个有符号的 16 位数量，在设计空间。 如果该字体为光栅字体，设计空间和设备空间是相同的字体单位等效于像素之间的距离。

基本上，IFIMETRICS 结构是文本指标结构的图形 DDI 版本。 所有的距离是指字体设计器的名义上的坐标系统。 名义空间坐标系统是惯用右手的笛卡尔坐标系统，在其中 y 坐标会增加顶部附近的和向右增加的 x 坐标。

IFIMETRICS 结构旨在为可变长度。 放置与字体相关的字符字符串的长度没有限制。 它是常见的做法来存储紧跟 IFIMETRICS 结构的最后一个字段的字符串。

提供了字体任何驱动程序必须支持[ **DrvQueryFont** ](https://msdn.microsoft.com/library/windows/hardware/ff556262)函数。 该驱动程序还可以包含函数[ **DrvQueryFontData** ](https://msdn.microsoft.com/library/windows/hardware/ff556264)来检索有关已实现的字体的信息。 在调用*DrvQueryFontData*，GDI 提供一个指针指向的标志符号或字距调整句柄数组。 该驱动程序返回有关关联的标志符号中信息 GDI [ **GLYPHDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff566819)结构。 如果*DrvQueryFontData*已给定的字距调整句柄，它返回有关字距调整对形式的 Win32 POINTL 结构信息。 下表列出了字体指标函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556192" data-raw-source="[&lt;strong&gt;DrvDestroyFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556192)"><strong>DrvDestroyFont</strong></a></p></td>
<td align="left"><p>该驱动程序可以释放它分配了所有的数据结构以便不再需要字体实现通知驱动程序。 GDI 调用此函数一次针对字体生成者，一次用于字体使用者。 可选-应支持，仅当该驱动程序必须释放已分配的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556226" data-raw-source="[&lt;strong&gt;DrvFree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556226)"><strong>DrvFree</strong></a></p></td>
<td align="left"><p>告知驱动程序不再需要所指示的数据结构。 应实现可选-，仅当驱动程序的内存管理需要使用此信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556262" data-raw-source="[&lt;strong&gt;DrvQueryFont&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556262)"><strong>DrvQueryFont</strong></a></p></td>
<td align="left"><p>返回一个指向<a href="https://msdn.microsoft.com/library/windows/hardware/ff567418" data-raw-source="[&lt;strong&gt;IFIMETRICS&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff567418)"> <strong>IFIMETRICS</strong> </a>字体的结构。 所需的处理与字体的所有驱动程序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556264" data-raw-source="[&lt;strong&gt;DrvQueryFontData&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556264)"><strong>DrvQueryFontData</strong></a></p></td>
<td align="left"><p>返回有关已实现的字体的信息。 所需 (针对选定<em>iMode</em>值) 的处理与字体的所有驱动程序。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff556266" data-raw-source="[&lt;strong&gt;DrvQueryFontTree&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff556266)"><strong>DrvQueryFontTree</strong></a></p></td>
<td align="left"><p>返回指向为定义的结构映射从 Unicode 标志符号的句柄或字距调整对到字距调整句柄的映射。 所需的处理与字体的所有驱动程序。</p></td>
</tr>
</tbody>
</table>

 

该函数*DrvQueryFontTree*允许 GDI，若要获取指向定义以下项之一的树状结构的指针：

-   从 Unicode 映射到字形句柄，包括象形文字变体 (GDI [ **FD\_GLYPHSET** ](https://msdn.microsoft.com/library/windows/hardware/ff565625)结构)

-   映射的字距调整对到字距调整句柄 ([**FD\_KERNINGPAIR** ](https://msdn.microsoft.com/library/windows/hardware/ff565630)结构)

*DrvQueryFontTree*需要付出努力来生成所需的结构，因此驱动程序应尽可能预先计算这些文件。 在资源中或在文件中，可以存储结构。 如果在文件中存储结构，用于加载或读取它们的理想方法是调用[ **EngMapFontFile** ](https://msdn.microsoft.com/library/windows/hardware/ff564972)函数，它指向的内存映射文件。 并不能获取该文件附加到交换文件，因为内存可提供必要时，这是比打开和读取的文件中更高效。

具体而言，驱动程序将返回中的标识符*pid*参数。 GDI 将其传递给[ **DrvFree** ](https://msdn.microsoft.com/library/windows/hardware/ff556226)函数，返回的指针时[ **FD\_GLYPHSET** ](https://msdn.microsoft.com/library/windows/hardware/ff565625)结构或数组[ **FD\_KERNINGPAIR** ](https://msdn.microsoft.com/library/windows/hardware/ff565630)不再需要结构。 具体取决于如何在该驱动程序中管理内存*pid*可以标识结构，确定如何结构已分配，或根本不执行任何操作。

[**DrvFree** ](https://msdn.microsoft.com/library/windows/hardware/ff556226)并[ **DrvDestroyFont** ](https://msdn.microsoft.com/library/windows/hardware/ff556192)是这两个可选函数。 GDI 调用*DrvFree*来通知该驱动程序不再需要指定的数据结构。 该驱动程序不需要实现它，除非它为结构分配内存并需要在相应的数据结构可以将其释放时得到通知。 例如，如果与关联的数据[ **FONTOBJ** ](https://msdn.microsoft.com/library/windows/hardware/ff565974)结构，删除可能延迟到调用*DrvDestroyFont*，因此它不会为必需实现*DrvFree*。

*DrvDestroyFont*字体实现不再需要该驱动程序可以释放它分配了所有的数据结构以便将通知驱动程序。 GDI 调用此函数一次针对字体生成者，一次用于字体使用者。 仅当该驱动程序必须释放已分配的资源时销毁该字体实例应实现它。

 

 





