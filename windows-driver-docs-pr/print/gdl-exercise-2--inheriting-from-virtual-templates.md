---
title: GDL 练习 2 中的虚拟模板继承
description: GDL 练习 2 中的虚拟模板继承
ms.assetid: 89878438-bea4-4d6f-bf3b-88d5bef0e6ab
keywords:
- GDL WDK 示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK 教程
- WDK GDL，实现 GDL 架构的架构
- 模板 WDK GDL，继承
- 模板 WDK GDL，示例
- 继承 WDK GDL
- WDK GDL 的虚拟模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 530c5f3606da5bebbac7cbba59a25a5fd6470484
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369796"
---
# <a name="gdl-exercise-2-inheriting-from-virtual-templates"></a>GDL 练习 2：从虚拟模板继承


### <a href="" id="exercise"></a> 练习

定义接受通过使用 2 个字节来表示 1 个 Unicode 字符编码的 Unicode 字符串数据类型。 然后，定义非虚拟继承以前定义的虚拟模板的模板。 请不要修改中创建的架构[练习 1](gdl-exercise-1--implementing-a-gdl-schema.md)。 创建示例 GDL 数据文件，并验证正确应用架构。 创建一个示例 GDL 数据文件，不符合的架构，验证检测到错误。

### <a href="" id="solution"></a> 解决方案

以下两个模板定义的 Unicode 数据类型。

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

以下模板继承在练习 1 中定义的模板。 没有名为的构造\*命令和三种类型的属性：**\*名称**（将显示在根级别），  **\*CommandName** (其中可以出现在\*命令构造)，和 **\*UniName** （后者可以显示两个上下文中）。

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

 

 




