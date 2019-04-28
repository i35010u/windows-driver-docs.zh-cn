---
title: 模拟字体属性
description: 模拟字体属性
ms.assetid: 000f3c30-2e8a-41b7-ac06-6f2da550ac70
keywords:
- 模拟的字体属性 WDK Unidrv
- 字体属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9073d4dac718d942ab0ca9c596e34c875200facd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331184"
---
# <a name="attributes-for-simulated-fonts"></a>模拟字体属性





下表列出了属性描述模拟字体的打印机的支持。

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
<td><p><strong>*DiffFontsPerByteMode?</strong></p></td>
<td><p><strong>TRUE</strong>或<strong>FALSE</strong>。 对于支持单字节和双字节模式的打印机，这指示打印机是否维护单独的字体和字体特征的每种模式。</p></td>
<td><p>可选。 如果未指定，默认值是<strong>FALSE</strong>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅[示例 GPD 文件](sample-gpd-files.md)。

 

 




