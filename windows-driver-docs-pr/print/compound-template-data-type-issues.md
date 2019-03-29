---
title: 复合模板数据类型问题
description: 复合模板数据类型问题
ms.assetid: 61f26465-c79d-42e3-94c8-26c2c61ecb98
keywords:
- 模板 WDK GDL，数据类型
- 数据类型 WDK GDL，模板的数据类型的问题
- 数据类型 WDK GDL，复合
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b54f141501b36833db2ead1b1da50e730b11931
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562939"
---
# <a name="compound-template-data-type-issues"></a>复合模板数据类型问题


复合数据类型都从其他数据类型创建并使用括号括起的数据类型之一，也必须由括号括括起来的括号括起来的数据类型的所有数据类型。

例如，假设您通过使用以下模板定义 GPD 整数列表。

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

然后，以下值是有效和等效表达式的列表\_OF\_列表\_OF\_整数数据类型。

```cpp
*ListList: 1,2,3:10,11,12:20,21,22 
*ListList: (1,2,3:10,11,12:20,21,22)
*ListList: ((1,2,3):(10,11,12):(20,21,22))
```

但是，下面的值违反了嵌套的括号规则。

```cpp
*ListList: (1,2,3):(10,11,12):(20,21,22)
```

前面的示例将生成语法错误的下一步括号分析器筛选器假定遇到任何括号属于最外层的上下文，因为属于下一步上下文中，依次类推。

 

 




