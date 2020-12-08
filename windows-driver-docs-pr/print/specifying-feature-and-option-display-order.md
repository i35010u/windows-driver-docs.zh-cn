---
title: 指定功能和选项显示顺序
description: 指定功能和选项显示顺序
keywords:
- Unidrv、功能和选项显示顺序
- 功能的显示顺序/选项 WDK Unidrv
- 属性表页 WDK 打印、功能和选项显示顺序
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ad6a6bba8bcd0788856590b23c60a755f520066
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806913"
---
# <a name="specifying-feature-and-option-display-order"></a>指定功能和选项显示顺序





若要控制功能和选项在 Unidrv 生成的属性页上的显示顺序，请 \* \* 在 GPD 文件中包含空功能和选项项。 在完整 \* 功能和选项条目的外观之前 \* 以及对功能或选项名称的任何其他引用之前，必须将这些项放在文件开头。 列出空条目的顺序是功能和选项在属性表页上的显示顺序。 但 (注意，PaperSize 功能的选项始终按字母顺序列出，此顺序不能更改。 ) 

下面是一组空 \* 功能和选项条目的示例 \* ：

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

该示例指定显示 EconoMode、方向、PaperSize 和分辨率功能的顺序。 此外，它还指定 EconoMode、方向和分辨率选项的显示顺序。 PaperSize 选项按字母顺序显示。

如果 GPD 文件未包含用于 \* 指定显示顺序的空功能和 \* 选项条目，则 GPD 分析器会确定显示顺序。 尽管分析器通常会使功能和选项按其在 GPD 文件中出现的顺序显示，但不保证此顺序。 此外，默认情况下，分析器始终导致 InputBin 功能首先显示。

建议包含空的 \* 功能和 \* 选项条目来显式指定显示顺序，而不允许分析器创建订单。

 

 




