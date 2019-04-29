---
title: 打印机 INF 文件的即插即用 ID
description: 打印机 INF 文件的即插即用 ID
ms.assetid: 4adb9203-1267-466e-89d8-63988ffa56e9
keywords:
- INF 文件 WDK 打印，插 Id
- 即插即用 ID WDK 打印
- 插 Id WDK 打印
- 标识符 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29d5f01490e2e88445e036c1849949588d9208ab
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380253"
---
# <a name="plug-and-play-ids-for-printer-inf-files"></a>打印机 INF 文件的即插即用 ID


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
<td><p>该 ID 始终是特定的具有 ID 字符串中的"1394"。</p></td>
</tr>
<tr class="even">
<td><p>并行</p></td>
<td><p>该 ID 包含"LPTENUM&amp;q u o t;中的 ID 字符串。</p></td>
</tr>
<tr class="odd">
<td><p>USB</p></td>
<td><p>该 ID 包含"USBPRINT&amp;q u o t;中的 ID 字符串。</p></td>
</tr>
<tr class="even">
<td><p>Dot4</p></td>
<td><p>该 ID 包含"DOT4PRT&amp;q u o t;中的 ID 字符串。 此 ID 适用于 Dot4USB 和并行。 .</p></td>
</tr>
<tr class="odd">
<td><p>蓝牙</p></td>
<td><p>该 ID 包含"BTHPRINT&amp;q u o t;中的 ID 字符串。</p></td>
</tr>
<tr class="even">
<td><p>WSD</p></td>
<td><p>该 ID 包含"WSDPRINT&amp;q u o t;中的 ID 字符串。</p></td>
</tr>
</tbody>
</table>

 

 

 




