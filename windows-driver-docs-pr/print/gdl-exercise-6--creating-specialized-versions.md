---
title: GDL 练习6创建专用版本
description: GDL 练习6创建专用版本
keywords:
- GDL WDK，示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK，教程
- 构造 WDK GDL，创建专用版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 931c4b928ec437346609a90002721e4dc19ab293
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796995"
---
# <a name="gdl-exercise-6-creating-specialized-versions"></a>GDL 练习6：创建专用版本


### <a name="exercise"></a><a href="" id="exercise"></a> 小心谨慎

使用 [练习 5](gdl-exercise-5--defining-name-limits-for-different-features.md)，为 PFeature 创建 POption 的三个专用版本 \* \* ： PaperSize。

-   第一个版本用于实例名称为 "Papersize"、"法律" 和 "A4" 的选项。 这些选项将具有当前行为。

-   第二个版本用于实例名称为 "Custom" 的 Papersize 选项，并将识别以下附加属性： **\* MinSize** 和 **\* MaxSize**。

-   第三个版本将包含其他 papersize 选项，这些选项将被视为 OEM 定义，并将识别其他属性： **\* OEM \_ 信息**。

进行此更改，而不删除或修改任何先前定义的模板。 创建一个简单的 GDL 数据文件，以验证是否正确 templatization 了条目。

### <a name="solution"></a><a href="" id="solution"></a> 解决方案

下面的代码示例演示了一个可能的答案。

```cpp
*Template:  MIN_SIZE
{
    *Name: "*MinSize"
    *Type:  ATTRIBUTE
    *ValueType:  PAGE_DIM
}
*Template:  MAX_SIZE
{
    *Name: "*MaxSize"
    *Type:  ATTRIBUTE
    *ValueType:  PAGE_DIM
}

*Template:  OEM_INFO
{
    *Name: "*OEM_Info"
    *Type:  ATTRIBUTE
    *ValueType:  NORMAL_STRING
}


*Template:  OEM_PAPERSIZE_OPTION
{
    *Inherits: PAPERSIZE_OPTION2
    *Members:  (OEM_INFO)
    *Instances:  <ANY>
}
*Template:  CUST_PAPERSIZE_OPTION
{
    *Inherits: PAPERSIZE_OPTION2
    *Members:  (MIN_SIZE, MAX_SIZE)
    *Instances:  Custom
}
*Template:  PREDEFINED_PAPERSIZE_OPTION
{
    *Inherits: PAPERSIZE_OPTION2
    *Instances:  (Letter, Legal, A4)
}
```

下面的代码示例演示用于验证的示例 GDL 数据文件。

```cpp
*PFeature: random
{
    *Name:  "Generic Feature"
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
        *PaperSize: PAIR(8.5, 11) ,  inches
    }
    *POption:   Legal
    {
        *Name: "Legal"
        *Command: "Select Legal"
        *PaperSize: PAIR(8.5, 14) ,  inches
    }
    *POption: A4
    {
        *Name: "A4"
        *Command: "Select A4"
        *PaperSize: PAIR(205, 317),  mm
    }
    *POption: OEMName_Special_size
    {
        *Name: "OEMName size"
        *Command: "Select OEMName size"
        *PaperSize: PAIR(365, 487), mm
        *OEM_Info: "<83 d4 93 ae>"
    }

    *POption: Custom
    {
        *Name: "Custom Size"
        *Command: "Select Custom"
        *MaxSize: PAIR(400, 500), mm
        *MinSize: PAIR(100, 150), mm
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
        *Capacity:  2000  *% sheets
    }
    *POption: Lower
    {
        *Name: "Lower Tray"
        *Command:  "Select Lower Tray"
        *Capacity:  500 *% sheets
    }
}
```

 

 




