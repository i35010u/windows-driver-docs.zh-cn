---
title: 定义配置相关的数据参数
description: 定义配置相关的数据参数
ms.assetid: a5bb2e3a-22e0-41d7-8035-5437ac473b21
keywords:
- GDL WDK 配置
- 配置 WDK GDL，定义依赖于配置的数据
- 定义配置依赖于数据 WDK GDL
- PICKMANY 参数 WDK GDL
- PICKONE 参数 WDK GDL
- null 值参数 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa01a83fcfbe0e3da71bb46b010c9ad1c2b0ad22
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342883"
---
# <a name="defining-the-configuration-dependent-data-parameters"></a>定义配置相关的数据参数


通过引入参数 **\*功能**构造。 构造标记 **\*功能**构造标识的参数 (或定义的参数名称，也称为*功能名称*)。

内容 **\*功能**构造可以包含一个或多个 **\*选项**构造。 **\*选项**构造定义允许的值或参数可以是中的状态。 构造标记 **\*选项**构造标识允许的值或状态。 此构造标记也称为*选项名称*。

例如，可以定义一个名为参数*今天*，可能需要作为其值，如以下代码示例所示星期几。:

```cpp
*Feature: Today
{
  *Option: Sunday{}
  *Option: Monday{}
  *Option: Tuesday{}
  *Option: Wednesday{}
  *Option: Thursday{}
  *Option: Friday{}
  *Option: Saturday{}
}
```

在前面的示例中，*今天*参数可以采用在任何给定时间只有一个值。 *今天*不能既是**星期日**并**星期二**。 但是，并非所有参数并不局限于独占值;它们可以一次采用一个或多个值。 例如，如果必须在同一时间可容纳多个颜色笔在其现有的机器人，你可以定义*PenColors*参数来描述当前正在其现有的颜色。 您可以指定**PenColors:（红色和绿色和黄色）** 并且可能完全有效。

**\*UIType**保留的指令，您可以指定是否仅在任何时间 (PICKONE) 的单个值或是否多个值可以分配给该参数在给定的时间 (PICKMANY)，可能需要一个参数。 **\*UIType**指令位于为的子条目 **\*功能**构造。

**请注意**   GDL 不允许分配给参数"nothing"。 因此，若要描述保存没有笔机器人，必须声明一个称为无的选项或关闭 PICKMANY 参数。 使用的选项名称并不重要;您可以指定通过使用此属性指定哪些选项 **\*NoneOption**指令。 选项的 **\*NoneOption**指定与任何其他选项不兼容。

 

可以定义任意多个 **\*功能**构造具有参数。 所有 **\*功能**构造必须驻留在*根上下文*。 根上下文具有构造没有父级。

 

 




