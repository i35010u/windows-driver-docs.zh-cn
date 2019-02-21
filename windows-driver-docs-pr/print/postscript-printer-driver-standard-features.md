---
title: PostScript 打印机标准功能
description: 所提供的大多数 PostScript 打印机的常见事件的 PostScript 打印机标准功能。
ms.assetid: F904B8DD-7790-44FA-8C20-BCC3720B3528
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 075b940e4adef181f2abf875bb4501d39116ea10
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523430"
---
# <a name="postscript-printer-standard-features"></a>PostScript 打印机标准功能


所提供的大多数 PostScript 打印机的常见事件的 PostScript 打印机标准功能。

标准功能由 PPD 语言识别的预定义名称和下表显示了这些功能名称与在 PPD 文件中使用的标准关键字之间的映射。

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
<th>备注</th>
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
<td><p>页的排序规则</p>
<ul>
<li><p>逐份打印</p></li>
<li><p>未逐份打印</p></li>
</ul></td>
<td><p>可选</p>
<p>如果未指定，则不支持排序规则。</p></td>
</tr>
<tr class="even">
<td>JCLResolution</td>
<td>PageResolution</td>
<td>页面分辨率</td>
<td>至少一种类型的解析功能 （JCLResolution 或解析） 是必需的。 必须指定至少一个选项。</td>
</tr>
<tr class="odd">
<td><p>Duplex</p>
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
<p>如果未指定，则只将单个单面的打印支持。</p></td>
</tr>
<tr class="even">
<td>InputSlot</td>
<td>JobInputBin</td>
<td>类型的送纸盒</td>
<td><p>必需</p>
<p>自定义的送纸器名称必须是 24 个字符或更少。</p></td>
</tr>
<tr class="odd">
<td>MediaType</td>
<td>PageMediatype</td>
<td>类型的打印介质</td>
<td><p>可选</p>
<p>如果未指定，则始终使用打印机的默认值。</p></td>
</tr>
<tr class="even">
<td>OutputBin</td>
<td>JobOutputBin</td>
<td>类型的输出纸盒</td>
<td><p>可选</p>
<p>如果未指定，打印系统不会尝试选择收纸器。</p></td>
</tr>
<tr class="odd">
<td>PageSize</td>
<td>PageMediaSize</td>
<td>纸张大小</td>
<td><p>必需</p>
<p>必须指定至少一个选项。</p></td>
</tr>
<tr class="even">
<td>装订</td>
<td>JobStapleAllDocuments</td>
<td>装订的类型</td>
<td>可选</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[Pscript 微型驱动程序](pscript-minidrivers.md)  
[标准选项](standard-options.md)  



