---
title: Direction
description: Direction
ms.assetid: 19aa1c88-968d-4789-89cc-00b76b1a30d9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 128f89fd1fabbd08524d3adf634292aa9a5346d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342837"
---
# <a name="direction"></a>Direction


架构路径：\\Printer.Layout.NumberUp.Direction

节点类型： 属性

说明： 属性，用于确定在其中多个逻辑页放置在介质的顺序。 此属性的子值包含当前方向和打印设备支持的说明进行操作的列表。

Direction 属性包含两个对子值：CurrentValue 和支持。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespan-currentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span> CurrentValue

架构路径：\\Printer.Layout.NumberUp.Direction:CurrentValue

节点类型： 值

数据类型： BIDI\_字符串

说明： 在其中进行布局的逻辑页的当前 （默认值） 方向。 每个可能值包括水平方向和垂直方向。

下表列出了可能的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>ReplTest1</th>
<th>定义</th>
<th>逻辑页序 (4Up)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RightDown</p></td>
<td><p>打印在水平行，与工作表，顶部的第一行中的逻辑页数，后续行更低时打印工作表上。 在每个行中，从右到左打印逻辑页。</p></td>
<td><p>2 1</p>
<p>4 3</p></td>
</tr>
<tr class="even">
<td><p>DownRight</p></td>
<td><p>打印在垂直列中，右端的工作表，最接近的第一列的逻辑页并发现更远列保留在工作表上。 在每一列从上到下打印逻辑页。</p></td>
<td><p>3 1</p>
<p>4 2</p></td>
</tr>
<tr class="odd">
<td><p>LeftDown</p></td>
<td><p>打印在水平行，与工作表，顶部的第一行中的逻辑页数，后续行更低时打印工作表上。 在每个行中，从左到右打印逻辑页。</p></td>
<td><p>1 2</p>
<p>3 4</p></td>
</tr>
<tr class="even">
<td><p>DownLeft</p></td>
<td><p>在工作表上进一步向右打印在垂直列中，有左侧和右侧的工作表，最接近的第一列和后续列中的逻辑页。 在每一列从上到下打印逻辑页。</p></td>
<td><p>1 3</p>
<p>2 4</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsupportedspanspan-idsupportedspan-supported"></a><span id="supported"></span><span id="SUPPORTED"></span> 支持

架构路径：\\Printer.Layout.NumberUp.Direction:Supported

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个以逗号分隔列表的所有方向的支持的值。

 

 




