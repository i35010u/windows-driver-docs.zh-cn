---
title: 复合模板数据类型问题
description: 复合模板数据类型问题
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，模板数据类型的问题
- 数据类型 WDK GDL，复合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faa0e340f264ecd6e97231184c2757ecba43996e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797601"
---
# <a name="compound-template-data-type-issues"></a>复合模板数据类型问题


如果从其他数据类型创建复合数据类型，并使用括号将其中一种数据类型括起来，则括在括号内的所有数据类型都必须括在括号内。

例如，假设你使用以下模板来定义 GPD 整数的列表。

```cpp
*Template:  LIST_OF_INTS
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  INTEGER
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (int)
    *ArraySize: *
}
*Template:  LIST_OF_LIST_OF_INTS
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  LIST_OF_INTS
    *RequiredDelimiter: ":"
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (IntList)
    *ArraySize: *
}
```

然后，以下值是 \_ \_ \_ \_ 整数数据类型列表的有效和等效表达式。

```cpp
*ListList: 1,2,3:10,11,12:20,21,22 
*ListList: (1,2,3:10,11,12:20,21,22)
*ListList: ((1,2,3):(10,11,12):(20,21,22))
```

但是，以下值违反了括号规则的嵌套。

```cpp
*ListList: (1,2,3):(10,11,12):(20,21,22)
```

前面的示例将生成语法错误，因为分析器筛选器假设其遇到的任何括号属于最外层上下文，下一个括号属于下一个上下文，依此类推。

 

 




