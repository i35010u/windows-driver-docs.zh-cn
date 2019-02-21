---
title: Plug and Play Id 打印机 INF 文件
description: Plug and Play Id 打印机 INF 文件
ms.assetid: 4adb9203-1267-466e-89d8-63988ffa56e9
keywords:
- INF 文件 WDK 打印，插 Id
- 即插即用 ID WDK 打印
- 插 Id WDK 打印
- 标识符 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe581d2784461db3c7248c93c7883690a36020a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526558"
---
# <a name="plug-and-play-ids-for-printer-inf-files"></a>Plug and Play Id 打印机 INF 文件


必须指定[插](plug-and-play-for-printers.md)(PnP) 中的标识符 (Id)[打印机 INF 文件安装部分](printer-inf-file-install-sections.md)。

下表，具体取决于打印机使用的协议中，您必须使用 Id。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>协议</th>
<th>打印机 INF 文件中的即插即用 ID。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IEEE 1394</p></td>
<td><p>ID 始终是特定的与&quot;1394年&quot;ID 字符串中。</p></td>
</tr>
<tr class="even">
<td><p>并行</p></td>
<td><p>该 ID 包含&quot;LPTENUM&amp;q u o t; ID 字符串中。</p></td>
</tr>
<tr class="odd">
<td><p>USB</p></td>
<td><p>该 ID 包含&quot;USBPRINT&amp;q u o t; ID 字符串中。</p></td>
</tr>
<tr class="even">
<td><p>Dot4</p></td>
<td><p>该 ID 包含&quot;DOT4PRT&amp;q u o t; ID 字符串中。 此 ID 适用于 Dot4USB 和并行。 .</p></td>
</tr>
<tr class="odd">
<td><p>蓝牙</p></td>
<td><p>该 ID 包含&quot;BTHPRINT&amp;q u o t; ID 字符串中。</p></td>
</tr>
<tr class="even">
<td><p>WSD</p></td>
<td><p>该 ID 包含&quot;WSDPRINT&amp;q u o t; ID 字符串中。</p></td>
</tr>
</tbody>
</table>

 

 

 




