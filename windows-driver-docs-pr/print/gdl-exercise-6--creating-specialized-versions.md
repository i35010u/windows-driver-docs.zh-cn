---
title: GDL 练习 6 创建专用化版本
description: GDL 练习 6 创建专用化版本
ms.assetid: d9e60958-58b6-4ffe-a955-bc1b13b6a649
keywords:
- GDL WDK 示例
- 示例 WDK GDL
- 教程 WDK GDL
- GDL WDK 教程
- 构造 WDK GDL，创建的特殊的版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f62f1c624cbec11cb4665e1c0c3cbae514b34c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375600"
---
# <a name="gdl-exercise-6-creating-specialized-versions"></a>GDL 练习 6：创建专用版本


### <a href="" id="exercise"></a> 练习

使用[练习 5](gdl-exercise-5--defining-name-limits-for-different-features.md)，创建三个专用的版本\*POption 为\*PFeature:PaperSize。

-   有关 Letter、 法律和 A4 的实例名称 Papersize 选项是第一个版本。 这些选项会将它们的当前行为。

-   第二个版本是有关自定义的实例名称 Papersize 选项，并将识别以下附加特性：**\*MinSize**并 **\*MaxSize**。

-   第三个版本将介绍 OEM 定义并将识别的其他属性将被视为其他 papersize 选项：**\*OEM\_信息**。

进行此更改而不删除或修改任何以前定义的模板。 创建简单的 GDL 数据文件，以验证条目的适当操作。

### <a href="" id="solution"></a> 解决方案

下面的代码示例显示了一个可能的答案。

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

下面的代码示例显示了示例 GDL 数据文件进行验证。

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

 

 




