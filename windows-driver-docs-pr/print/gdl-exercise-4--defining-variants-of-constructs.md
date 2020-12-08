---
title: GDL 练习4定义构造的变体
description: GDL 练习4定义构造的变体
keywords:
- GDL WDK，示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK，教程
- 构造 WDK GDL，创建构造
- 创建 GDL 构造 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: faddbda5a9c1f27d2767ac8927143e5ec976afff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796997"
---
# <a name="gdl-exercise-4-defining-variants-of-constructs"></a>GDL 练习4：定义构造的变体


### <a name="exercise"></a><a href="" id="exercise"></a> 小心谨慎

\*定义两个变量： [Exercise 3](gdl-exercise-3--creating-root-level-constructs.md) \* PFeature： PaperSize 和 PFeature InputTray，从练习3修改构造 PFeature \* 。

PFeature 中包含的 POption \* 具有以下属性： **\* Name**、 **\* Command**、 **\* PaperSize**。

PFeature 中包含的 POption \* 具有以下属性： **\* 名称**、 **\* 命令** 和 **\* 容量：** *\# 工作表*。

创建一个模板来抽象这两种类型的 POptions 的通用属性 \* 。

### <a name="solution"></a><a href="" id="solution"></a> 解决方案

以下模板满足条件。

```cpp
*Template:  COMMAND_TYPE
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "COMMAND_STRING"
}
*Template:  ACOMMAND
{
    *Name:  "*Command"
    *Type:  ATTRIBUTE
    *ValueType:  COMMAND_TYPE
}
```

以下派生选项模板进一步定义虚拟模板 POPTION 的属性。

```cpp
*Template:  GENERIC_OPTION
{
    *Inherits: POPTION
    *Members:  (NAME, ACOMMAND)
    *Instances:  <ANY>
}
*Template:  XML_INT4
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "int"
}
*Template:  INTEGER
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_INT4
    *FilterTypeName: "HEX_OR_INT"
}
*Template:  XML_FLOAT
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "float"
}
*Template:  PAIR_OF_FLOAT
{
    *Type:  DATATYPE
    *DataType:   ARRAY
    *ElementType:  XML_FLOAT
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ArrayLabel: "PAIR"
    *ElementTags: (width, height)
    *ArraySize: 2
}
*Template:  LEN_UNITS
{
    *Type:  DATATYPE
    *DataType:   ENUMERATOR
    *XMLDataType: "LengthUnits"
    *EnumeratorList: (inches, mm, microns, pixels)
}
*Template:  PAGE_DIM
{
    *Type:  DATATYPE
    *DataType:   COMPOSITE
    *ElementType: (PAIR_OF_FLOAT, LEN_UNITS)
    *RequiredDelimiter: ","
    *OptionalDelimiter: "<20 09>"
    *ElementTags: (dimensions, units)
}
*Template:  PAPERDIMENSIONS
{
    *Name: "*PaperSize"
    *Type:  ATTRIBUTE
    *ValueType:  PAGE_DIM
}
```

以下派生选项模板进一步专用化模板通用选项的属性 \_ 。

```cpp
*Template:  PAPERSIZE_OPTION
{
    *Name:  "*POption"  *%  Isolate branch from Base Templates
    *Inherits: GENERIC_OPTION
    *Members:  (PAPERDIMENSIONS)
    *Instances:  <ANY>
}


*Template:  PAPERSIZE_FEATURE
{
    *Inherits: PFEATURE
    *Members:  (PAPERSIZE_OPTION)
    *Instances:  PaperSize
}

*Template:  TRAY_CAPACITY
{
    *Name: "*Capacity"
    *Type:  ATTRIBUTE
    *ValueType:  INTEGER
}
```

以下派生选项模板进一步专用化模板通用选项的属性 \_ 。

```cpp
*Template:  INPUTTRAY_OPTION
{
    *Name:  "*POption"   *%  Isolate branch from Base Templates
    *Inherits: GENERIC_OPTION
    *Members:  (TRAY_CAPACITY)
    *Instances:  <ANY>
}

*Template:  INPUTTRAY_FEATURE
{
    *Inherits: PFEATURE
    *Members:  (INPUTTRAY_OPTION)
    *Instances:  InputTray
}
```

 

 




