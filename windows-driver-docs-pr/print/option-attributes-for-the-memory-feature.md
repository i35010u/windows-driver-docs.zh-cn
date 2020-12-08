---
title: 内存功能的选项属性
description: 内存功能的选项属性
keywords:
- 内存功能 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 108a254c67625641223911fc2e54c92adba3793d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807721"
---
# <a name="option-attributes-for-the-memory-feature"></a>内存功能的选项属性





下表列出了与内存功能关联的属性： 有关内存功能的详细信息，请参阅 [标准功能](standard-features.md)。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>特性参数</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>MemConfigKB</strong></p></td>
<td><p>指示打印机驻留的总数和可用内存的数字值，以 kb 为单位。 例如，配对 (1024，450) 指示 1024 kb 450，可用大小为 "1024KB" 的 GPD。</p></td>
<td><p>可选。 请参阅 <a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MemConfigMB</strong></p></td>
<td><p>指示打印机驻留的总数和可用内存的数字值，以 mb 为单位。 例如，配对 (2，1) 指示 2 mb 总计，1 mb 可用，GPD 生成的选项名称为 "2MB"。</p></td>
<td><p>可选。 请参阅 <a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
<tr class="odd">
<td><p>*<strong>MemoryConfigKB</strong></p></td>
<td><p>指示打印机驻留的总数和可用内存的数字值，以 kb 为单位。 例如，配对 (1024，450) 指示 1024 kb，可用大小为 450 kb。</p></td>
<td><p>可选。 请参阅 <a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

有关使用这些属性的详细信息以及示例，请参阅 [描述打印机内存配置](describing-printer-memory-configurations.md)。

有关其他选项属性的信息，请参阅 [所有功能的选项属性](option-attributes-for-all-features.md)。

 

 




