---
title: 方向
description: 方向
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85e9f79c62581db490458dd021af63a5a095e897
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797209"
---
# <a name="direction"></a>方向


架构路径： \\ NumberUp。

节点类型：属性

说明：用于确定多个逻辑页面在媒体上的放置顺序的属性。 此属性的子值包含当前方向和打印设备所支持的方向列表。

Direction 属性包含两个子值： CurrentValue 和受支持。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespan-currentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span> CurrentValue

架构路径： \\ NumberUp： CurrentValue

节点类型：值

数据类型：双向 \_ 字符串

说明：当前 (默认) 方向， () 的逻辑页面布局。 每个可能的值由水平方向和垂直方向组成。

下表列出了可能的值。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>值</th>
<th>定义</th>
<th>逻辑页面顺序 (4Up) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>RightDown</p></td>
<td><p>在水平行中打印逻辑页，在工作表的顶部显示第一行，并在工作表的下部打印后续行。 在每行中，按从右到左的逻辑页面打印。</p></td>
<td><p>2 1</p>
<p>4 3</p></td>
</tr>
<tr class="even">
<td><p>DownRight</p></td>
<td><p>在垂直列中打印逻辑页面，第一列离工作表的右侧，后面的列离工作表。 在每列中，逻辑页从上到下打印。</p></td>
<td><p>3 1</p>
<p>4 2</p></td>
</tr>
<tr class="odd">
<td><p>LeftDown</p></td>
<td><p>在水平行中打印逻辑页，在工作表的顶部显示第一行，并在工作表的下部打印后续行。 在每行中，按从左到右的逻辑页面打印。</p></td>
<td><p>1 2</p>
<p>3 4</p></td>
</tr>
<tr class="even">
<td><p>DownLeft</p></td>
<td><p>在垂直列中打印逻辑页面，第一列离工作表的左侧，后面的列在工作表的右侧。 在每列中，逻辑页从上到下打印。</p></td>
<td><p>1 3</p>
<p>2 4</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idsupportedspanspan-idsupportedspan-supported"></a><span id="supported"></span><span id="SUPPORTED"></span> 受

架构路径： \\ NumberUp：支持

节点类型：值

数据类型：双向 \_ 字符串

说明：一个逗号分隔列表，其中列出了方向支持的所有值。

 

 




