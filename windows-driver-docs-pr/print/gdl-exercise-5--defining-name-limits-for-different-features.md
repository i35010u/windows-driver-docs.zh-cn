---
title: GDL 练习5定义不同功能的名称限制
description: GDL 练习5定义不同功能的名称限制
keywords:
- GDL WDK，示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK，教程
- 模板 WDK GDL，定义名称限制
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7e145a75653cec4c892c6bece295c02988de8a8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835963"
---
# <a name="gdl-exercise-5-defining-name-limits-for-different-features"></a>GDL 练习5：定义不同功能的名称限制


### <a name="exercise"></a><a href="" id="exercise"></a> 小心谨慎

使用 [练习 4](gdl-exercise-4--defining-variants-of-constructs.md)中的模板，定义在 \* POption 中显示的名称：构造，该构造 \* 是 \* PFeature： InputTray 的一部分，因此，最大长度限制为16个字符，并且 \* 名称：显示在 \* PFeature： PaperSize 中的 POption 内 \* 最多可包含24个字符。

进行此更改，而不删除或修改任何先前定义的模板。 创建一个简单的 GDL 数据文件，以验证是否正确 templatization 了条目。

### <a name="solution"></a><a href="" id="solution"></a> 解决方案

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

**注意**   使用 [继承](gdl-template-inheritance.md)，可以进一步优化和派生基类上的变体，而无需更改以前的模板所建立的架构的目的，也不会破坏。 此功能是继承的另一个优点。 继承为第三方提供了在不更改或违反 master 架构的情况下扩展 master 架构的能力。

 

 

 




