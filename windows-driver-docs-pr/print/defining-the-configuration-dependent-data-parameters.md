---
title: 定义配置相关的数据参数
description: 定义配置相关的数据参数
keywords:
- GDL WDK，配置
- 配置 WDK GDL，定义依赖于配置的数据
- 定义依赖于配置的数据 WDK GDL
- PICKMANY 参数 WDK GDL
- PICKONE 参数 WDK GDL
- null 值参数 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7321652e81e22246e5399e63d9782469dff1f380
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797299"
---
# <a name="defining-the-configuration-dependent-data-parameters"></a>定义配置相关的数据参数


使用 **\* Features** 构造引入参数。 **\* Features** 构造的构造标记标识参数 (或定义参数名称，该参数也称为 *功能名称*) 。

**\* 功能** 构造的内容可以包含一个或多个 **\* 选项** 构造。 **\* 选项** 构造定义参数可以位于的允许值或状态。 **\* 选项** 构造的构造标记标识了允许的值或状态。 此构造标记也称为 *选项名称*。

例如，可以定义一个名为 " *今天* " 的参数，该参数可以使用一周中的某一天作为其值，如以下代码示例所示：

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

在前面的示例中，在任何给定时间， *Today* 参数只能有一个值。 *今天* 不能同时为 **星期日** 和 **星期二**。 但是，并非所有参数都限制为独占值;它们一次可以接受一个或多个值。 例如，如果您的机器人可以同时拥有多个笔颜色，则可以定义一个 *PenColors* 参数来描述当前正在其手中的颜色。 你可以指定 **PenColors： (红色、绿色和黄色)** 并且可能完全有效。

**\* UIType** reserved 指令使你可以指定参数在任何时候都只能采用单个值 (PICKONE) 还是在给定的时间 (PICKMANY) 指定多个值。 **\* UIType** 指令将作为 **\* Features** 构造的子条目定位。

**注意**   GDL 不允许向参数分配 "nothing"。 因此，若要说明不包含任何笔的机器人，必须为 PICKMANY 参数声明一个名为 None 或 Off 的选项。 使用的选项名称并不重要;您可以使用 **\* NoneOption** 指令指定为其分配了该属性的选项。 **\* NoneOption** 指定的选项与其他任何选项都不兼容。

 

可以定义任意数量的 **\* 功能** 构造，因为有参数。 所有 **\* 功能** 构造必须位于 *根上下文* 中。 根上下文没有父构造。

 

 




