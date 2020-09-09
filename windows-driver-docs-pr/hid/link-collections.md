---
title: 链接集合
description: 链接集合
ms.assetid: 3f934661-c33c-4c08-82ac-ee2e0f519c8e
keywords:
- 链接集合 WDK HID
- 嵌套集合 WDK HID
- 链接集合数组 WDK HID
- 化名为的集合 WDK HID
- 链接集合节点 WDK HID
- 阵列 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b72b4d017d6f6ae05e5d4c97c441b14c87ad2c1
ms.sourcegitcommit: 9145bffd4cc3b990a9ebff43b588db6ef2001f5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/09/2020
ms.locfileid: "89592399"
---
# <a name="link-collections"></a>链接集合





作为[顶级集合](top-level-collections.md)中嵌套子集合的*链接集合*。 顶级集合可以有零个或多个链接集合。

[**HidP \_GetLinkCollectionNodes**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getlinkcollectionnodes) 返回顶级集合的 [链接集合数组](#ddk-link-collection-array-kg) ，其中包含有关顶级集合的链接集合的信息。

### <a name="link-collection-array"></a><a href="" id="ddk-link-collection-array-kg"></a>链接集合数组

*链接集合数组*介绍了顶层集合中包含的所有链接集合。 每个链接集合均由一个 [**HIDP \_ 链接 \_ 集合 \_ 节点**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_link_collection_node) 结构表示。 数组的链接节点以在顶级集合中标识顺序和分层顺序的方式进行链接。 链接集合数组的第一个元素表示顶级集合，其余成员表示顶级集合的链接集合。

通过跟踪链接连接数组中的节点，用户模式应用程序或内核模式驱动程序可以确定顶级集合中的所有链接集合的组织和使用情况。 此外，应用程序或驱动程序可以按其链接集合来组织控件。 这是可能的，因为顶级集合的 [按钮功能数组](button-capability-arrays.md) 和 [值功能数组](value-capability-arrays.md) 标识包含功能数组所述的每个 [HID 使用情况](hid-usages.md) 的链接集合。

下图显示了一个包含四个链接集合的顶级集合的示例。

![阐释包含四个链接集合的顶级集合的关系图](images/linkcol.png)

如上图所示，链接集合按从上到下、从左到右的顺序链接在一起 (ABCD) 。 下表列出了示例中的每个链接集合的顶级集合及其链接集合之间的链接。

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
<th>Parent</th>
<th>子女</th>
<th>First Child</th>
<th>下一个同级</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A</p></td>
<td><p>顶级集合</p></td>
<td><p>B、C</p></td>
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

 

在链接集合数组中，以下定义保留：

<a href="" id="parent"></a>**上层**  
链接集合的 *父级* 是位于集合的从上到下层次结构中的紧上方的集合。 链接集合具有一个父项。 链接节点的 **父** 成员指定链接集合数组中其父级的索引。

<a href="" id="children"></a>**观看**  
链接集合是其父项的 *子项* 。 父代可以有零个或多个子级。 Link 节点的 **NumberOfChildren** 成员指定父项的子项数。

<a href="" id="sibling"></a>**同级**  
父级的子级是 *同级*。

<a href="" id="next-sibling"></a>**下一个同级**  
同级按从左到右的顺序排列。 同级的 *下一个同级* 元素是紧靠同级的同级元素。 链接集合节点的 **NextSibling** 成员指定其在链接集合数组中的下一个同级的索引。 如果链接集合节点没有下一个同级，则 **NextSibling** 设置为零。

<a href="" id="first-child"></a>**第一个子**  
*第一个子级*是同级中的最左侧同级。 链接集合节点的 **FirstChild** 成员指定链接集合数组中第一个子级的索引。 如果链接集合节点没有任何子节点，则将 **FirstChild** 设置为零。

应用程序或驱动程序可以通过从父项的第一个子级开始，确定父集合的所有子级，并从第一个子级的同级节点序列化，直到同级节点的 **NextSibling** 成员为零。

下面的代码演示如何使用链接集合节点索引查找链接集合7的第一个子元素：

```cpp
HIDP_LINK_COLLECTION_NODE Collection[10] ;
HIDP_LINK_COLLECTION_NODE Node1 ;
 
Node1 = Collection[Collection[7].FirstChild]] ;
```

### <a name="aliased-collections"></a><a href="" id="aliased-collections"></a> 别名集合

可以在报表描述符中使用分隔符项来分隔一组化名为的 *集合*。 每个别名集均由一个别名链接集合节点表示。 完全和唯一的一组*n* *n* &gt; = 2，别名节点通过以下方式链接在一起：

-   别名节点在链接集合数组中按顺序排列。

-   前 *n*个节点的 **IsAlias** 成员设置为 **TRUE**。 紧跟此类序列的第 *n* 个节点将其 **IsAlias** 成员设置为 **FALSE**。 此节点终止化名为的节点序列。 与此节点关联的使用情况是首选用法。

应用程序或驱动程序可以通过重复递增链接集合数组的数组索引来确定哪些集合是别名的，以便查找这样的序列。

[按钮功能数组](button-capability-arrays.md) 和 [值功能数组](value-capability-arrays.md) 标识每个使用情况的链接集合。 如果链接集合具有别名，则功能阵列指定首选用法。

 

