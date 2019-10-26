---
title: TTD 集合对象
description: 本部分介绍与时间行程调试关联的范围模型对象。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd66ce58d402f6462db2a245aee607ec99e712af
ms.sourcegitcommit: 8e8aa927cf4ab56d0af652fa5e988a8ed6967904
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2019
ms.locfileid: "72916224"
---
# <a name="ttd-collection-objects"></a>TTD 集合对象

> [!NOTE]
> 本主题中的信息是初步文档。 文档的更高版本中将提供更新的信息。
>

## <a name="description"></a>描述

## <a name="children"></a>Children


| 对象 | 描述 |
| --- | --- |
| MinPosition | 一个[位置对象](time-travel-debugging-position-objects.md)，该对象描述与范围相关的最早位置。 |

### <a name="ttd-collection-object-methods"></a>TTD 集合对象方法

**Contains （OtherString）** -返回字符串是否包含给定的子字符串的方法。

**EndsWith （OtherString）** -返回字符串是否以给定字符串结尾的方法。

**IndexOf （OtherString）** -返回给定字符串中某个子字符串的第一个匹配项的索引的方法。  如果不存在此类事件，则返回-1。

**LastIndexOf （OtherString）** -返回给定字符串中某个子字符串的最后一个匹配项的索引的方法。  如果不存在此类事件，则返回-1。

**Length** -属性，它返回字符串的长度。

**PadLeft （TotalWidth）** -通过在字符串左侧插入空格，将字符串右对齐指定宽度的方法。

**PadRight （TotalWidth）** -一种方法，该方法通过在字符串的右侧插入空格，将字符串与指定的宽度对齐。

**Remove （StartPos，[Length]）** -方法，该方法从字符串中删除从指定位置开始的所有字符。  如果提供了可选长度，则仅删除起始位置后的多个字符。

**Replace （SearchString，ReplaceString）** -方法，该方法将每个指定的搜索字符串替换为替换字符串。

**StartsWith （OtherString）** -返回字符串是否以给定字符串开头的方法。

**Substring （StartPos，[Length]）** -从给定字符串中检索子字符串的方法。  子字符串从指定的字符位置开始，并继续到字符串的末尾或指定的指定长度。

**ToLower （）** -返回此字符串转换为小写形式的副本。

**ToUpper （）** -返回此字符串转换为大写形式的副本。

## <a name="example-usage"></a>示例用法

*待处理信息*



## <a name="see-also"></a>另请参阅

[旅行调试-时间行程调试对象简介](time-travel-debugging-object-model.md)

[行程调试-概述](time-travel-debugging-overview.md)
