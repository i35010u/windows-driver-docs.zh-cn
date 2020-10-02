---
title: TTD 集合对象
description: 了解与时间行程调试关联的范围模型对象。 请参阅示例使用情况和查看其他可用资源。
ms.date: 09/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a1a1dd9ecb0b8d561d46cffcdb49b9c1c207941
ms.sourcegitcommit: 372464be981a39781c71049126f36891cb5d0cad
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91646137"
---
# <a name="ttd-collection-objects"></a>TTD 集合对象

> [!NOTE]
> 本主题中的信息是初步文档。 文档的更高版本中将提供更新的信息。
>

## <a name="description"></a>说明

## <a name="children"></a>子女


| Object | 说明 |
| --- | --- |
| MinPosition | 一个 [位置对象](time-travel-debugging-position-objects.md) ，该对象描述与范围相关的最早位置。 |

### <a name="ttd-collection-object-methods"></a>TTD 集合对象方法

**包含 (OtherString) ** 方法，该方法返回字符串是否包含给定的子字符串。

**EndsWith (OtherString) ** 方法，该方法返回字符串是否以给定字符串结尾。

**IndexOf (OtherString) ** 方法，该方法返回给定字符串中某个子字符串的第一个匹配项的索引。  如果不存在此类事件，则返回-1。

**LastIndexOf (OtherString) ** 方法，该方法返回给定字符串中某个子字符串的最后一个匹配项的索引。  如果不存在此类事件，则返回-1。

**Length** -属性，它返回字符串的长度。

**PadLeft (TotalWidth) ** 方法，该方法通过在字符串的左侧插入空格将字符串右对齐指定的宽度。

**PadRight (TotalWidth) ** 方法，该方法通过在字符串的右侧插入空格，将字符串与指定的宽度对齐。

**删除 (StartPos，[Length] ) 方法， ** 该方法从字符串中删除从指定位置开始的所有字符。  如果提供了可选长度，则仅删除起始位置后的多个字符。

**替换 (SearchString，ReplaceString) 方法， ** 该方法用替换字符串替换指定的搜索字符串的每个匹配项。

**StartsWith (OtherString) ** 方法，该方法返回字符串是否以给定字符串开头。

**子字符串 (StartPos，[Length] ) ** -从给定字符串中检索子字符串的方法。  子字符串从指定的字符位置开始，并继续到字符串的末尾或指定的指定长度。

**ToLower ( # B1 ** -返回此字符串转换为小写形式的副本。

**ToUpper ( # B1 ** -返回此字符串转换为大写形式的副本。

## <a name="example-usage"></a>示例用法

*待处理信息*



## <a name="see-also"></a>另请参阅

[时光穿越调试 - 时光穿越调试对象简介](time-travel-debugging-object-model.md)

[时光穿越调试 - 概述](time-travel-debugging-overview.md)
