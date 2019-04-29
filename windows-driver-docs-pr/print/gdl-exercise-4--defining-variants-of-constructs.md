---
title: GDL 练习 4 个定义的变体的构造
description: GDL 练习 4 个定义的变体的构造
ms.assetid: b923b5f8-6e60-44a0-a38e-8bfa315281c5
keywords:
- GDL WDK 示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK 教程
- 构造 WDK GDL，创建构造
- 创建 GDL 构造 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19a52c47e71acdf59224d7694e434f67094b30d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375607"
---
# <a name="gdl-exercise-4-defining-variants-of-constructs"></a>GDL 练习 4：定义构造的变体


### <a href="" id="exercise"></a> 练习

修改构造\*从 PFeature[练习 3](gdl-exercise-3--creating-root-level-constructs.md)通过定义两种变体：\*PFeature:PaperSize 和\*PFeature InputTray。

中包含 POption \*PFeature:PaperSize 具有以下属性：**\*名称**， **\*命令**，  **\*Papersize**。

中包含 POption \*PFeature:InputTray 具有以下属性：**\*名称**， **\*命令**，并**\*容量：**  *\#表的*。

创建模板以抽象的这两种类型的通用属性\*POptions。

### <a href="" id="solution"></a> 解决方案

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

进一步的以下派生的选项模板定义虚拟模板 POPTION 的属性。

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

进一步的以下派生的选项模板专用化模板通用的属性\_选项。

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

进一步的以下派生的选项模板专用化模板通用的属性\_选项。

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

 

 




