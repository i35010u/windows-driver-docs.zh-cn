---
title: 模拟字体属性
description: 模拟字体属性
keywords:
- 模拟字体特性 WDK Unidrv
- 字体属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03043f809716232063cd01a72fc892e7037c4ae4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836111"
---
# <a name="attributes-for-simulated-fonts"></a>模拟字体属性





下表列出了描述打印机对模拟字体的支持的属性。

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
<td><p><strong>*DiffFontsPerByteMode?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 对于支持单字节和双字节模式的打印机，这指示打印机是否为每个模式维护单独的字体和字体特征。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。</p></td>
</tr>
</tbody>
</table>

 

有关示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

 

 




