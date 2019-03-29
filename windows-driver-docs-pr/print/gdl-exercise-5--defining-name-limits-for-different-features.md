---
title: GDL 练习 5 定义名称限制为不同的功能
description: GDL 练习 5 定义名称限制为不同的功能
ms.assetid: 8e6c59d7-c748-4133-ba70-e5be413bae54
keywords:
- GDL WDK 示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK 教程
- 模板 WDK GDL，定义命名限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd23569edcce53cec862af2adbe17cb9352d546d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567783"
---
# <a name="gdl-exercise-5-defining-name-limits-for-different-features"></a>GDL 练习 5：定义不同功能的名称限制


### <a href="" id="exercise"></a> 练习

使用中的模板[练习 4](gdl-exercise-4--defining-variants-of-constructs.md)，定义\*名称： 出现在构造\*属于 POption \*PFeature:InputTray 使其限制为 16 个字符最大值和\*名称： 出现在\*POption 属于\*PFeature:PaperSize 被限制为 24 个字符最大值。

进行此更改而不删除或修改任何以前定义的模板。 创建简单的 GDL 数据文件，以验证条目的适当操作。

### <a href="" id="solution"></a> 解决方案

以下模板满足条件。

```cpp
*Template:  PAPER_SIZE_OPT_NAME
{
*Name:  "*Name"  *% isolate this branch from base templates
*Inherits: NAME
*MaxLength: 24 chars
}
*Template:  INPUTTRAY_OPT_NAME
{
*Name:  "*Name"  *% isolate this branch from base templates
*Inherits: NAME
*MaxLength: 16 chars
}

*Template:  INPUTTRAY_OPTION2
{
    *Inherits: INPUTTRAY_OPTION
    *Members:  (INPUTTRAY_OPT_NAME)
    *Instances:  <ANY>
}
*Template:  PAPERSIZE_OPTION2
{
    *Inherits: PAPERSIZE_OPTION
    *Members:  (PAPER_SIZE_OPT_NAME)
    *Instances:  <ANY>
}
*PFeature: random
{
*Name:"Generic Feature"
*DefaultOption: First
*POption: First
{
 *Name: "First Option"
 *Command: "Select me"
}
}
*PFeature: PaperSize
{
*Name: "Paper Size"
*DefaultOption: Letter
*POption: Letter
{
 *Name: "Letter"
 *Command: "Select Letter"
 *PaperSize: PAIR(8.5, 11) inches
}
*POption:   Legal
{
 *Name: "Legal"
 *Command: "Select Legal"
 *PaperSize: PAIR(8.5, 14) inches
}
*POption: A4
{
 *Name: "A4"
 *Command: "Select A4"
 *PaperSize: PAIR(205, 317) mm
}
}
*PFeature: InputTray
{
*Name:  "Paper Source"
*DefaultOption: Upper
*POption: Upper
{
 *Name: "Upper Tray"
 *Command:  "Select Upper Tray"
 *Capacity:  2000 sheets
}
*POption: Lower
{
 *Name: "Lower Tray"
 *Command:  "Select Lower Tray"
 *Capacity:  500 sheets
}
}
```

**请注意**   Using[继承](gdl-template-inheritance.md)，可以进一步细化和派生基类的变体，而无需更改任何以前的模板或通过破坏的架构的意图的上一模板建立。 此功能是继承的另一个优势。 继承提供了第三方扩展主架构而无需更改或违反主架构的功能。

 

 

 




