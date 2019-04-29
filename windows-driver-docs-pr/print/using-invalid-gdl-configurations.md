---
title: 使用无效的 GDL 配置
description: 使用无效的 GDL 配置
ms.assetid: a61232dd-ab64-4ca4-9eb9-68fe5c7249e4
keywords:
- GDL WDK 配置
- 配置 WDK GDL，无效的配置
- 无效 GDL 配置 WDK
- 配置 WDK GDL，示例
- InvalidCombination 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1226ffd071ea12c837db07467e22700111368188
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387131"
---
# <a name="using-invalid-gdl-configurations"></a>使用无效的 GDL 配置


并非所有可能的设置包括无效或不允许。 例如，打印设备可能不允许某个项硬性媒体，放入任何送纸器，因为媒体可能卡纸。 GDL 语言，可通过定义的无效的参数设置的组合还定义无效配置。

\*InvalidCombination 指令用于此目的。 值\*InvalidCombination 是名称不能一起使用的两个或多个参数设置的列表。 用来指定参数设置的语法是以 EBNF 表示法，如以下代码示例所示。

```cpp
InvalidCombination_Directive :== "*InvalidCombination" S ":"  S ParamSettingsList  S LB
ParamSettingsList :== "LIST" S "("  S ParamSetting S ","  S ParamSetting ( S "," S ParamSetting)?  S ")"
ParamSetting :== ParameterName "." Value
ParameterName :== {Construct Tag of *Feature construct}
Value :==  {Construct Tag of *Option construct found within the *Feature construct.}
S :== [#x20#x09]*
LB :== [#x0A] | [#x0D] | ([#x0A] [#x0D]) | ([#x0D] [#x0A])
```

\*InvalidCombination 指令必须出现在 GDL 文件的根上下文。

例如如果你想要防止在周末下雨，则可以指定下面的代码。

```cpp
*InvalidCombination: LIST(Weather.Rain, Today.Saturday)
*InvalidCombination: LIST(Weather.Rain, Today.Sunday)
```

如果您希望在周末防止下雨，仅当时运行正常，则可以指定下面的代码。

```cpp
*InvalidCombination: LIST(Weather.Rain, Today.Saturday, Health.Well)
*InvalidCombination: LIST(Weather.Rain, Today.Sunday, Health.Well)
```

\*InvalidCombination 指令前面的代码示例中指定任何包含的特定组合 （Weather.Rain、 Today.Sunday、 Health.Well 或 Weather.Rain、 Today.Saturday、 Health.Well） 的配置违反了指令。

\*InvalidCombination 指令为特定类型的约束。 GDL 分析器函数确定提供的配置是否与任何继续操作之前 GDL 文件中定义的约束冲突。 如果检测到冲突时，配置是修改 （或解析） 以避免违反了约束。 这种情况称为[解析约束](resolving-gdl-configuration-conflicts.md)。 在单个 GDL 文件中可能存在数百个涉及几十个参数的约束。 约束可以形成复杂 web 的交互，以便在一个参数的设置的更改可能会更改的连环导致其他参数。

**请注意**  必须确保默认配置不违反任何约束。 如果是这样，任何分析器接口函数将会成功。

 

**请注意**   GDL 分析器还接受的一种特殊情况\*InvalidCombination 涉及只有两个参数设置。

 

 

 




