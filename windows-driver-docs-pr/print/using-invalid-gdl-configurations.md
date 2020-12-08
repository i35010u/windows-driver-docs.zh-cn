---
title: 使用无效的 GDL 配置
description: 使用无效的 GDL 配置
keywords:
- GDL WDK，配置
- 配置 WDK GDL，配置无效
- 无效的 GDL 配置 WDK
- 配置 WDK GDL，示例
- InvalidCombination 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f17b53a1b117d527db2d80dfedf34b22037cd9b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785985"
---
# <a name="using-invalid-gdl-configurations"></a>使用无效的 GDL 配置


并非所有可能的配置都有效或不允许。 例如，打印设备可能不允许将硬性介质放入任何输入纸盒，因为介质可能会卡住。 使用 GDL 语言，还可以通过定义无效的参数设置组合来定义无效的配置。

\*InvalidCombination 指令用于实现此目的。 InvalidCombination 的值 \* 是一个列表，它将不能一起使用的两个或多个参数设置命名为。 用于指定参数设置的语法采用 EBNF 表示法，如以下代码示例所示。

```cpp
InvalidCombination_Directive :== "*InvalidCombination" S ":"  S ParamSettingsList  S LB
ParamSettingsList :== "LIST" S "("  S ParamSetting S ","  S ParamSetting ( S "," S ParamSetting)?  S ")"
ParamSetting :== ParameterName "." Value
ParameterName :== {Construct Tag of *Feature construct}
Value :==  {Construct Tag of *Option construct found within the *Feature construct.}
S :== [#x20#x09]*
LB :== [#x0A] | [#x0D] | ([#x0A] [#x0D]) | ([#x0D] [#x0A])
```

\*InvalidCombination 指令必须出现在 GDL 文件的根上下文中。

例如，如果想要在周末阻止 rain，可以指定以下代码。

```cpp
*InvalidCombination: LIST(Weather.Rain, Today.Saturday)
*InvalidCombination: LIST(Weather.Rain, Today.Sunday)
```

如果只想在周末阻止 rain，则可以指定以下代码。

```cpp
*InvalidCombination: LIST(Weather.Rain, Today.Saturday, Health.Well)
*InvalidCombination: LIST(Weather.Rain, Today.Sunday, Health.Well)
```

\*前面的代码示例中的 InvalidCombination 指令指定包含特定组合 (的任何配置（即，) ，即 "当前"、"当前" 或 ""。

\*InvalidCombination 指令是特定类型的约束。 GDL 分析器函数确定所提供的配置是否违反 GDL 文件中定义的任何约束，然后再继续。 如果检测到冲突，则 (或已解决) 修改配置，以避免违反约束。 这种情况称为 ["解析约束"](resolving-gdl-configuration-conflicts.md)。 包含数十个参数的数百个约束可能存在于单个 GDL 文件中。 约束可以构成复杂的交互 web，以便一个参数的设置更改可能导致在其他参数中出现层叠更改。

**注意**   必须确保默认配置不违反任何约束。 如果是这样，则任何分析器接口函数都不会成功。

 

**注意**   GDL 分析器还接受 \* 只涉及两个参数设置的 InvalidCombination 的一种特殊情况。

 

 

 




