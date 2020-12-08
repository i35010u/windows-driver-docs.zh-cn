---
title: GDL 练习2从虚拟模板继承
description: GDL 练习2从虚拟模板继承
keywords:
- GDL WDK，示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK，教程
- 架构 WDK GDL，实现 GDL 架构
- 模板 WDK GDL，继承
- 模板 WDK GDL，示例
- 继承 WDK GDL
- 虚拟模板 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f6fb4047cf0dc1d5753415dc073aee16915f7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797001"
---
# <a name="gdl-exercise-2-inheriting-from-virtual-templates"></a>GDL 练习2：从虚拟模板继承


### <a name="exercise"></a><a href="" id="exercise"></a> 小心谨慎

定义一个数据类型，该数据类型接受通过使用2个字节来表示1个 Unicode 字符编码的 Unicode 字符串。 然后，定义从以前定义的虚拟模板继承的非虚拟模板。 不要修改您在 [练习 1](gdl-exercise-1--implementing-a-gdl-schema.md)中创建的架构。 创建示例 GDL 数据文件，并验证是否正确应用了架构。 创建不符合架构的示例 GDL 数据文件，并验证是否检测到错误。

### <a name="solution"></a><a href="" id="solution"></a> 解决方案

以下两个模板定义 Unicode 数据类型。

```cpp
*Include: MasterTemplate.gdl
 
*Template:  XML_STRING
{
    *Type:  DATATYPE
    *DataType:   XML_TYPE
    *XMLDataType: "string"
}
```

```cpp
*Template:  NORMAL_STRING
{
    *Type:  DATATYPE
    *DataType:   FILTER_TYPE
    *ElementType:  XML_STRING
    *FilterTypeName: "NORMAL_STRING"
}
```

以下模板继承自练习1中定义的模板。 存在一个名为 \* "命令" 的构造和三种类型的属性： "名称" (，该 **\* 名称** 出现在根级别) 、 **\* CommandName** (，可以出现在 \* 命令构造) 中，并可在两个上下文 (中出现。 **\***

```cpp
*Template:  COMMAND
{
    *Name:  "*Command"
    *Inherits: CONSTRUCTS
    *Instances:  <ANY>
}
*Template:  ROOT_NAME
{
    *Name:  "*Name"
    *Inherits: ROOT_ATTRIB
    *ValueType:  NORMAL_STRING
}
*Template:  CMD_NAME
{
    *Name:  "*CommandName"
    *Inherits: CONSTRUCT_ATTRIB
    *ValueType:  NORMAL_STRING
}
*Template:  UNIVERSAL_NAME
{
    *Name:  "*UniName"
    *Inherits: FREEFLOAT
    *ValueType:  NORMAL_STRING
}
```

以下 GDL 文件符合给定的架构。

```cpp
*Name: "can only appear at root level"
*UniName:  "can appear anywhere"
*Command: X
{
    *CommandName:  "May only appear within a command"
    *UniName:  "can appear anywhere, even in a command"
    *Command: nested
    {
        *CommandName:  "nested commands are ok."
        *UniName:  "template defined a recursive nesting" 100 %
    }
}
```

以下 GDL 文件不符合给定的架构。

```cpp
*CommandName:  "Error! May only appear within a command"
*Command: X
{
    *Name: "Error! can only appear at root level"
}
```

 

 




