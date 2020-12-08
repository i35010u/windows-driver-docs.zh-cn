---
title: GDL 练习说明
description: GDL 练习说明
keywords:
- GDL WDK，示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK，教程
- GDL WDK，索引树
- 分析器 WDK GDL，索引树
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81befa64059327ca031bba53df0c0070fc9e4230
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835953"
---
# <a name="gdl-exercise-notes"></a>GDL 练习说明


下面的代码示例演示分析器为所有 GDL 练习生成的索引树。

```cpp
      <:ROOT2>
    *PFeature : InputTray    <:INPUTTRAY_FEATURE>
        *POption : Lower    <:INPUTTRAY_OPTION2>
            *Capacity    <:TRAY_CAPACITY>
            *Command    <:ACOMMAND>
            *Name    <:INPUTTRAY_OPT_NAME>
        *POption : Upper    <:INPUTTRAY_OPTION2>
            *Capacity    <:TRAY_CAPACITY>
            *Command    <:ACOMMAND>
            *Name    <:INPUTTRAY_OPT_NAME>
        *DefaultOption    <:DEFAULT_OPT>
        *Name    <:NAME>
    *PFeature : PaperSize    <:PAPERSIZE_FEATURE>
        *POption : Custom    <:CUST_PAPERSIZE_OPTION>
            *MinSize    <:MIN_SIZE>
            *MaxSize    <:MAX_SIZE>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : OEMName_Special_size    <:OEM_PAPERSIZE_OPTION>
            *OEM_Info    <:OEM_INFO>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : A4    <:PREDEFINED_PAPERSIZE_OPTION>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : Legal    <:PREDEFINED_PAPERSIZE_OPTION>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *POption : Letter    <:PREDEFINED_PAPERSIZE_OPTION>
            *PaperSize    <:PAPERDIMENSIONS>
            *Command    <:ACOMMAND>
            *Name    <:PAPER_SIZE_OPT_NAME>
        *DefaultOption    <:DEFAULT_OPT>
        *Name    <:NAME>
    *PFeature : random    <:PFEATURE >
        *POption : First    <:GENERIC_OPTION>
            *Command    <:ACOMMAND>
            *Name    <:NAME>
        *DefaultOption    <:DEFAULT_OPT>
        *Name    <:NAME>
```

\*Name 和 \* POption 条目映射到多个模板，每个模板都有不同的语义。 例如， \* name 映射为 name、INPUTTRAY \_ opt \_ name 或纸张 \_ 大小 \_ opt \_ name。 \*POption 映射到通用 \_ 选项、预定义的 \_ PAPERSIZE \_ 选项、 \_ PAPERSIZE \_ 选项、OEM \_ PAPERSIZE \_ 选项或 INPUTTRAY \_ 选项2。 如果已正确定义模板结构，则分析器将在其 templatization 规则后找到最适合的模板。

**注意**   这些练习将建立一些基本模板，随后会在架构变得更详细的同时派生出变体。 此过程模拟了架构在现实生活中的演变方式。 通过继承，可以在不更改任何以前定义的模板的情况下扩展练习架构。 此功能可让第三方扩展 master 架构，还可确保任何第三方架构扩展与原始主架构的用户保持兼容。

 

显示的练习答案不是唯一的。 例如，你可以 \_ \_ 通过以下方式从 PAPERDIMENSIONS 派生模板最小大小和最大大小。

```cpp
*Template:  MIN_SIZE
{
    *Name: "*MinSize"
    *Inherits: PAPERDIMENSIONS
}
*Template:  MAX_SIZE
{
    *Name: "*MaxSize"
    *Inherits: PAPERDIMENSIONS
}
```

请注意，纸张 \_ 大小 \_ opt \_ name 和 INPUTTRAY \_ OPT \_ name 模板从模板名称继承，并且还会重新定义 \* 名称条目。

重新定义 \* 名称条目的效果是，从基本模板建立的继承树中隐藏这些派生模板。

通常，当模板将名称声明为成员时 \* ，此声明表示从名称派生的所有模板也是 \* 成员。 但是，具有重新定义的 \* 名称项的派生模板将从 \* 派生模板的隐含成员列表中排除。 如果没有此排除项，将最初映射到模板名称的数据条目 (例如， \* 在 Pfeature) 中出现的名称 \* 将映射到 INPUTTRAY \_ OPT \_ 名称 (这) 不正确。

如果预计在架构的原始设计中将名称专用化到纸张 \_ 大小 \_ opt \_ name 和 INPUTTRAY \_ OPT \_ 名称中，则只需从通用选项的成员列表中删除名称，就会产生不同的架构实现 \* \_ 。 此更改不需要重新定义 \* 名称。 进一步的设计优化将具有名称、纸张 \_ 大小 \_ OPT \_ 名称和 INPUTTRAY \_ OPT \_ name （继承自公共虚拟模板），因为这种情况更准确地反映了这些关键字之间的关系。

 

 




