---
title: 指定功能和选项显示顺序
description: 指定功能和选项显示顺序
ms.assetid: 51e18121-540b-40f0-85f8-eb2755a583f7
keywords:
- Unidrv、 功能和选项显示顺序
- 功能/选项 WDK Unidrv 的显示顺序
- 属性表页 WDK 打印、 功能和选项显示顺序
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2acd8b8c621ce6c9822388c988778ff9dd59c7e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372066"
---
# <a name="specifying-feature-and-option-display-order"></a>指定功能和选项显示顺序





若要控制在其中功能和选项的显示的顺序 Unidrv 生成的属性表页上，包括空\*功能和\*选项 GPD 文件中的条目。 必须将这些条目放置文件的完整出现前开始\*功能和\*选项条目，和任何其他功能或选项的名称引用之前。 空项的列出顺序是在其中的功能和选项显示在属性表页的顺序。 （请注意，但是，始终按字母顺序列出 PaperSize 功能的选项，不能更改此顺序。）

下面是示例的一组空\*功能和\*选项条目：

```cpp
*Feature: EconoMode
{
    *Option: Off{}
    *Option: On{}
}
*Feature: Orientation
{
    *Option: PORTRAIT{}
    *Option: LANDSCAPE_CC90{}
}
*Feature: PaperSize
{
}
*Feature: Resolution
{
    *Option: Option1{}
    *Option: Option2{}
    *Option: Option3{}
}
```

该示例指定经济模式、 方向、 PaperSize，以及解析功能的显示的顺序。 此外，它指定经济模式、 方向和分辨率选项的显示顺序。 PaperSize 选项按字母顺序显示。

如果 GPD 文件不包括空\*功能和\*选项指定的显示顺序条目，GPD 分析器会认为的显示顺序。 功能和选项，以 GPD 文件中出现的顺序显示，通常都会导致分析器，而不保证此顺序。 此外，默认情况下分析程序始终会导致要首先显示的 InputBin 功能。

包括空\*功能和\*选项项以便显式指定显示建议通过允许分析器来创建顺序进行排序。

 

 




