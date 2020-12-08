---
title: PostScript 打印机标准功能
description: PostScript 打印机标准版功能是大多数 PostScript 打印机提供的常用功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84207160977a768d0dc448153e3e625d2fc0c019
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807531"
---
# <a name="postscript-printer-standard-features"></a>PostScript 打印机标准功能


PostScript 打印机标准版功能是大多数 PostScript 打印机提供的常用功能。

标准功能由 PPD 语言识别的预定义名称标识，下表显示了功能名称与 PPD 文件中使用的标准关键字之间的映射。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>功能名称</th>
<th>默认打印架构功能关键字</th>
<th>描述</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>逐份打印</p>
<ul>
<li><p>true</p></li>
<li><p>false</p></li>
</ul></td>
<td>DocumentCollate</td>
<td><p>页排序规则</p>
<ul>
<li><p>排序</p></li>
<li><p>彩色</p></li>
</ul></td>
<td><p>可选</p>
<p>如果未指定，则不支持排序规则。</p></td>
</tr>
<tr class="even">
<td>JCLResolution</td>
<td>PageResolution</td>
<td>页面分辨率</td>
<td>至少需要一种分辨率功能 (JCLResolution 或解决) 。 必须至少指定一个选项。</td>
</tr>
<tr class="odd">
<td><p>双工</p>
<ul>
<li><p>DuplexTumble</p></li>
<li><p>DuplexNoTumble</p></li>
<li><p>任何其他选项</p></li>
</ul></td>
<td>JobDuplexAllDocumentsContiguously</td>
<td><p>双面打印</p>
<ul>
<li><p>TwoSidedShortEdge</p></li>
<li><p>TwoSidedLongEdge</p></li>
<li><p>OneSided</p></li>
</ul></td>
<td><p>可选</p>
<p>如果未指定，则仅支持单面打印。</p></td>
</tr>
<tr class="even">
<td>InputSlot</td>
<td>JobInputBin</td>
<td>输入纸盒的类型</td>
<td><p>必须</p>
<p>自定义的输入箱名称必须小于或等于24个字符。</p></td>
</tr>
<tr class="odd">
<td>MediaType</td>
<td>PageMediatype</td>
<td>打印介质的类型</td>
<td><p>可选</p>
<p>如果未指定，则始终使用打印机的默认介质。</p></td>
</tr>
<tr class="even">
<td>OutputBin</td>
<td>JobOutputBin</td>
<td>输出容器类型</td>
<td><p>可选</p>
<p>如果未指定，则打印系统不会尝试选择一个输出 bin。</p></td>
</tr>
<tr class="odd">
<td>PageSize</td>
<td>PageMediaSize</td>
<td>纸张大小</td>
<td><p>必须</p>
<p>必须至少指定一个选项。</p></td>
</tr>
<tr class="even">
<td>装订</td>
<td>JobStapleAllDocuments</td>
<td>装订类型</td>
<td>可选</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[Pscript 微型驱动程序](pscript-minidrivers.md)  
[标准选项](standard-options.md)  



