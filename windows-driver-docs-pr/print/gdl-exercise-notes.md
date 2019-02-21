---
title: GDL 练习说明
description: GDL 练习说明
ms.assetid: 39013410-ad8e-4b1a-9db7-2ec541f08989
keywords:
- GDL WDK 示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK 教程
- GDL WDK，索引树
- 分析器 WDK GDL，索引树
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf8ee1ab3103d736f5b0939db3f9b032ea1f91e7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542969"
---
# <a name="gdl-exercise-notes"></a>GDL 练习说明


下面的代码示例显示了分析器会生成所有 GDL 练习在索引树。

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

\*名称和\*POption 条目映射到多个模板，每个都有不同的语义。 例如，\*名称将映射到名称，INPUTTRAY\_OPT\_名称或纸张\_大小\_OPT\_名称。 \*POption 映射到泛型\_选项、 预定义\_PAPERSIZE\_选项，CUST\_PAPERSIZE\_选项、 OEM\_PAPERSIZE\_选项或 INPUTTRAY\_选项 2。 如果已正确定义的模板结构，遵循其操作规则的分析器将查找最合适的模板。

**请注意**  练习建立一些基本模板和随后派生的变体变得更详细的架构。 此过程会模拟在现实生活中的架构不断发展的方式。 继承启用练习架构进行扩展，而无需更改任何以前定义的模板。 此功能，第三方扩展主架构，并且还可确保任何第三方架构扩展仍然符合原始主架构的用户。

 

显示的练习答案不是唯一的。 例如，你可能具有派生模板最小\_大小和最大\_PAPERDIMENSIONS 按以下方式从的大小。

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

请注意，本文\_大小\_OPT\_名称和 INPUTTRAY\_OPT\_名称模板从模板名称继承，并且还重新定义\*项命名。

重新定义的效果\*名称项是隐藏在基模板建立的继承树中这些派生的模板。

通常情况下，当模板声明名称，使\*成员，此声明表示从名称派生的所有模板也都是\*成员。 但是，使用派生的模板重新定义\*排除名称条目从默示\*成员派生模板列表。 而无需此排除将最初已映射到模板名称的数据条目 (例如，\*名称出现在\*Pfeature) 将映射到 INPUTTRAY\_OPT\_（这是不正确） 的名称。

如果希望在名称的专用化到文件\_大小\_OPT\_名称和 INPUTTRAY\_OPT\_将导致在架构中，不同的架构实现原始设计过程中的名称只需通过删除名称从\*成员列表泛型\_选项。 此更改会使用户无需重新定义\*名称。 进一步的设计优化将具有名称，纸张\_大小\_OPT\_名称和 INPUTTRAY\_OPT\_名称继承一个通用的虚拟模板，因为这种情况下更准确地反映了这些关键字之间的关系。

 

 




