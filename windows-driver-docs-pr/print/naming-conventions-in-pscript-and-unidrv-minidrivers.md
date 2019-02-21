---
title: Pscript 和 Unidrv 微型驱动程序中的命名约定
description: Pscript 和 Unidrv 微型驱动程序中的命名约定
ms.assetid: d15c72e9-781d-4c71-bcf5-b3d08ec603ca
keywords:
- 框中自动配置支持 WDK 打印机，命名约定
- 名称 WDK 打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d23c45a9d84f6728f456946a72679916f998e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520073"
---
# <a name="naming-conventions-in-pscript-and-unidrv-minidrivers"></a>Pscript 和 Unidrv 微型驱动程序中的命名约定


想要在其 Pscript5 或 Unidrv 微型驱动程序支持自动配置的硬件供应商必须遵循以下命名约定。 打印机说明文件应命名根据打印机的模型名称。 在本主题中所示的文件名&lt;printerModelName&gt;是打印机的型号名称的占位符。

### <a href="" id="pscript5-minidrivers"></a> Pscript5 微型驱动程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>文件类型</th>
<th>命名约定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要的打印机说明文件</p></td>
<td><p>&lt;printerModelName&gt;.PPD</p></td>
</tr>
<tr class="even">
<td><p>辅助打印机说明文件</p></td>
<td><p>&lt;printerModelName&gt;.GDL</p></td>
</tr>
</tbody>
</table>

 

辅助打印机说明文件包含 bidi 或自动配置信息。

若要启用自动配置，Pscript5 驱动程序必须包括&lt;printerModelName&gt;。GDL 和 ps\_schm。GDL 其依赖的文件列表中。 有关依赖文件的信息，请参阅[打印机 INF 文件条目](printer-inf-file-entries.md)。

### <a href="" id="unidrv-minidrivers"></a> Unidrv 微型驱动程序

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>文件类型</th>
<th>命名约定</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>主要的打印机说明文件</p></td>
<td><p>&lt;printerModelName&gt;。GPD 或&lt;printerModelName&gt;。GDL</p>
<p>使用文件的类型取决于所使用的打印机说明格式。</p></td>
</tr>
<tr class="even">
<td><p>辅助打印机说明文件 （可选）</p></td>
<td><p>&lt;printerModelName&gt;.GDL</p></td>
</tr>
</tbody>
</table>

 

辅助打印机说明文件，是可选的 Unidrv 微型驱动程序，该文件包含 bidi 或自动配置信息。 或者，可以在主要说明文件中包含自动配置信息。

若要启用自动配置，Unidrv 驱动程序必须包含任何&lt;printerModelName&gt;。GPD 或&lt;printerModelName&gt;。GDL 其依赖的文件列表，以及以下文件中的文件：

Stddtype.gdl

Stdschem.gdl

Stdschmx.gdl

 

 




