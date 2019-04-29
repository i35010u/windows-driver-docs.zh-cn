---
title: 内存功能的选项属性
description: 内存功能的选项属性
ms.assetid: 17646f6e-b234-4a17-ba24-4bc7f6f85ace
keywords:
- 内存功能 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 420532a2f91190afcc0d70bf7dcfdf2e43f42f30
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353711"
---
# <a name="option-attributes-for-the-memory-feature"></a>内存功能的选项属性





下表列出了与内存功能关联的属性。 有关内存功能的详细信息，请参阅[标准功能](standard-features.md)。

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
<th>备注</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em><strong>MemConfigKB</strong></p></td>
<td><p>对数字值，该值指示总计和可用驻留在打印机中的内存，以千字节。 例如，配对 (1024，450) 指示的总 1024 千字节为单位，可用，它包含"1024 KB"GPD 生成选项名称 450 千字节为单位。</p></td>
<td><p>可选。 请参阅<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
<tr class="even">
<td><p></em><strong>MemConfigMB</strong></p></td>
<td><p>对数字值，该值指示总计和可用驻留在打印机中的内存，用兆字节表示。 例如，对 （2，1） 指示 2 兆字节总计，可用，它包含"2 MB"GPD 生成选项名称 1 兆字节。</p></td>
<td><p>可选。 请参阅<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
<tr class="odd">
<td><p>*<strong>MemoryConfigKB</strong></p></td>
<td><p>对数字值，该值指示总计和可用驻留在打印机中的内存，以千字节。 例如，配对 (1024，450) 指示的总 1024 千字节为单位，用 450 千字节为单位。</p></td>
<td><p>可选。 请参阅<a href="describing-printer-memory-configurations.md" data-raw-source="[Describing Printer Memory Configurations](describing-printer-memory-configurations.md)">描述打印机内存配置</a>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

有关使用这些属性，以及一些示例，请参阅[描述打印机内存配置](describing-printer-memory-configurations.md)。

有关其他选项的属性的信息，请参阅[所有功能的选项属性](option-attributes-for-all-features.md)。

 

 




