---
title: TTD 集合对象
description: 本部分介绍与时间旅行调试关联的范围模型对象。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfe3301d049ad5b63e77b2da117332b2d3b680d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541240"
---
> [!NOTE]
> 本主题中的信息是初定版。 更新的信息将在文档中的更高版本的版本中提供。 
>

# <a name="ttd-collection-objects"></a>TTD 集合对象

## <a name="description"></a>描述

## <a name="children"></a>Children


| 对象 | 描述 |
| --- | --- |
| MinPosition | 一个[位置对象](time-travel-debugging-position-objects.md)，它描述与范围相关的最早位置。 |




### <a name="ttd-collection-object-methods"></a>TTD 集合对象方法


**Contains(OtherString)** -它将返回字符串是否包含给定的子字符串的方法。

**EndsWith(OtherString)** -它将返回字符串是否以给定字符串结尾的方法。

**IndexOf(OtherString)** -方法返回给定字符串中的子字符串的第一个匹配项的索引。  如果没有此类事件存在，则返回-1。

**LastIndexOf(OtherString)** -方法返回给定字符串中的子字符串的最后一个匹配项的索引。  如果没有此类事件存在，则返回-1。

**长度**-属性返回字符串的长度。

**PadLeft(TotalWidth)** -方法的右对齐到指定的宽度的字符串插入空格的字符串的左侧。

**PadRight(TotalWidth)** -方法的左对齐字符串的右侧插入空格指定宽度的字符串。

**删除 （正好从，[长度]）** -这将删除所有字符从字符串中的指定位置开始的方法。  如果可选长度所提供的仅删除多个字符的起始位置之后。

**替换 (SearchString，ReplaceString)** -使用替换字符串替换指定的搜索字符串的每个匹配项的方法。

**StartsWith(OtherString)** -它将返回字符串是否以给定字符串开头的方法。

**子字符串 （正好从，[长度]）** -从给定的字符串中检索子字符串的方法。  子字符串指定的字符位置开始，并继续到结尾的字符串或有选择地指定长度。

**Tolower （)** -返回此字符串的副本转换为小写。

**Toupper （)** -返回此字符串的副本转换为大写。

## <a name="example-usage"></a>示例用法

*挂起的信息*



## <a name="see-also"></a>另请参阅

[时间旅行调试-时间旅行调试对象简介](time-travel-debugging-object-model.md)

[按照时间顺序逐个调试-概述](time-travel-debugging-overview.md)

---


