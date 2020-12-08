---
title: Pscript 和 Unidrv 微型驱动程序中的命名约定
description: Pscript 和 Unidrv 微型驱动程序中的命名约定
keywords:
- 内置自动配置支持 WDK 打印机，命名约定
- 命名 WDK 打印机自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e587e4374ef1fdafe32acce0011dc6adc5947b77
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807819"
---
# <a name="naming-conventions-in-pscript-and-unidrv-minidrivers"></a>Pscript 和 Unidrv 微型驱动程序中的命名约定


要支持 Pscript5 或 Unidrv 微型驱动程序中的自动配置的硬件供应商必须遵循以下命名约定。 应按照打印机的型号名称命名打印机说明文件。 在本主题中显示的文件名中， &lt; printerModelName &gt; 是打印机型号名称的占位符。

### <a name="pscript5-minidrivers"></a><a href="" id="pscript5-minidrivers"></a> Pscript5 微型驱动程序

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
<td><p>主打印机说明文件</p></td>
<td><p>&lt;printerModelName &gt; 。信息库</p></td>
</tr>
<tr class="even">
<td><p>辅助打印机说明文件</p></td>
<td><p>&lt;printerModelName &gt; 。GDL</p></td>
</tr>
</tbody>
</table>

 

辅助打印机说明文件包含双向或自动配置信息。

若要启用自动配置，Pscript5 驱动程序必须包括 &lt; printerModelName &gt; 。GDL 和 ps \_ schm。GDL 的相关文件列表。 有关依赖文件的信息，请参阅 [打印机 INF 文件条目](printer-inf-file-entries.md)。

### <a name="unidrv-minidrivers"></a><a href="" id="unidrv-minidrivers"></a> Unidrv 微型驱动程序

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
<td><p>主打印机说明文件</p></td>
<td><p>&lt;printerModelName &gt; 。GPD 或 &lt; printerModelName &gt; 。GDL</p>
<p>使用的文件类型取决于所使用的打印机说明格式。</p></td>
</tr>
<tr class="even">
<td><p>辅助打印机说明文件 (可选) </p></td>
<td><p>&lt;printerModelName &gt; 。GDL</p></td>
</tr>
</tbody>
</table>

 

辅助打印机说明文件（对 Unidrv 微型驱动程序是可选的）包含双向或自动配置信息。 此外，自动配置信息可以包含在主说明文件中。

若要启用自动配置，Unidrv 驱动程序必须包含任何 &lt; printerModelName &gt; 。GPD 或 &lt; printerModelName &gt; 。GDL 文件在其相关文件列表中，以及以下文件：

Stddtype.gdl

Stdschem.gdl

Stdschmx.gdl

 

 




