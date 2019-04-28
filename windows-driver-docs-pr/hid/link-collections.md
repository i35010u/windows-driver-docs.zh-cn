---
title: 链接集合
description: 链接集合
ms.assetid: 3f934661-c33c-4c08-82ac-ee2e0f519c8e
keywords:
- 将集合 WDK HID 链接
- WDK HID 的嵌套的集合
- WDK HID 链接集合数组
- 使用别名集合 WDK HID
- 链接 WDK HID 集合节点
- WDK HID 的数组
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 417ee3c07732623ff66c5d3ef3fa4dc58dde7434
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346226"
---
# <a name="link-collections"></a>链接集合





一个*集合链接*作为嵌套子集合内[顶级集合](top-level-collections.md)。 顶级集合可以有零个或多个链接集合。

[**HidP\_GetLinkCollectionNodes** ](https://msdn.microsoft.com/library/windows/hardware/ff539725)返回的顶级集合[链接集合数组](#ddk-link-collection-array-kg)包含有关顶级集合的链接集合的信息。

### <a href="" id="ddk-link-collection-array-kg"></a>链接集合数组

一个*链接集合数组*介绍顶级集合内包含的所有链接集合。 每个链接集合表示由[ **HIDP\_链接\_集合\_节点**](https://msdn.microsoft.com/library/windows/hardware/ff539764)结构。 数组的链接节点标识顶级集合中的其顺序和分层顺序的方式链接。 链接集合数组的第一个元素表示顶级集合和其余成员表示顶级集合的链接集合。

通过跟踪通过链接连接数组中的节点中，用户模式应用程序或内核模式驱动程序可以确定组织和使用情况的顶级集合中的所有链接集合。 此外，应用程序或驱动程序可以控件通过组织他们链接集合。 这可能是因为顶级集合的[按钮功能数组](button-capability-arrays.md)并[值功能数组](value-capability-arrays.md)标识链接集合，其中包含每个[HID 用法](hid-usages.md)通过功能数组所述。

下图显示了包含四个链接集合的顶级集合的示例。

![说明包含四个链接集合的顶级集合的关系图](images/linkcol.png)

在上图中所示，链接集合是链接在一起顶部到底部中和从左到右的顺序 (ABCD)。 下表为在示例中，每个链接集合指示顶级集合的链接集合之间的链接。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>链接节点</th>
<th>Parent 的子磁盘）</th>
<th>Children</th>
<th>第一个子级</th>
<th>下一个同级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A</p></td>
<td><p>顶级集合</p></td>
<td><p>B, C</p></td>
<td><p>B</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>B</p></td>
<td><p>A</p></td>
<td><p>D</p></td>
<td><p>D</p></td>
<td><p>C</p></td>
</tr>
<tr class="odd">
<td><p>C</p></td>
<td><p>A</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
</tr>
<tr class="even">
<td><p>D</p></td>
<td><p>B</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
<td><p>无</p></td>
</tr>
</tbody>
</table>

 

在链接集合数组中，保留以下定义：

<a href="" id="parent"></a>**Parent**  
链接集合的*父*是顶部到底部层次结构中其上紧邻的集合的集合。 链接集合有一个父级。 **父**成员链接节点的链接集合数组中指定其父项的索引。

<a href="" id="children"></a>**Children**  
链接集合是*子*其父级。 父级可以有零个或多个子级。 **NumberOfChildren**链接节点的成员指定一个父节点有子级的个数。

<a href="" id="sibling"></a>**同级**  
父级的子级*同级*。

<a href="" id="next-sibling"></a>**下一个同级**  
同级按时间顺序从左到右。 同级*下一个同级*如果有一组同级中是紧挨其右侧的同级。 **NextSibling**成员链接集合节点的链接集合数组中指定到其下一个同级元素的索引。 如果链接集合节点不具有下一个同级元素， **NextSibling**设置为零。

<a href="" id="first-child"></a>**第一个子级**  
*第一个子级*是中一组同级成员的最左边的同级节点。 **FirstChild**成员链接集合节点的链接集合数组中指定其第一个子级的索引。 如果链接集合节点不具有任何子级**FirstChild**设置为零。

应用程序或驱动程序可以通过从父项的第一个子级，直到第一个子级的同级元素通过序列化开始来确定父集合的所有子级**NextSibling**成员的同级节点为零。

下面的代码演示如何使用链接集合节点索引来查找链接集合七的第一个子级：

```cpp
HIDP_LINK_COLLECTION_NODE Collection[10] ;
HIDP_LINK_COLLECTION_NODE Node1 ;
 
Node1 = Collection[Collection[7].FirstChild]] ;
```

### <a href="" id="aliased-collections"></a> 使用别名集合

分隔符项可用于报表描述符中分隔的一组*别名集合*。 使用别名链接集合节点表示每个别名集合。 一组完整且唯一的*n*， *n* &gt;= 2，使用别名节点中的以下方法链接在一起：

-   使用别名节点的链接集合数组中的连续顺序。

-   第一个*n*-1 节点具有其**IsAlias**成员设置为**TRUE**。 *第 n 个*紧跟此类序列的节点都有其**IsAlias**成员设置为**FALSE**。 此节点终止使用别名节点的顺序。 与此节点关联的用法是首选的用法。

应用程序或驱动程序可以确定哪些集合通过重复递增要找到此类序列的链接集合数组的数组索引是使用别名。

[按钮功能数组](button-capability-arrays.md)并[值功能数组](value-capability-arrays.md)标识、 为每个用途它们描述，包含使用情况的链接集合。 如果链接集合的别名，功能数组指定首选的用法。

 

 




