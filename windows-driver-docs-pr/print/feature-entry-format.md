---
title: 功能项格式
description: 功能项格式
keywords:
- 打印机功能 WDK Unidrv，输入格式
- 格式化 WDK 打印机功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc0c511a8c1c68a6a688a17258049d775be3f3bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836055"
---
# <a name="feature-entry-format"></a>功能项格式





若要在 GPD 文件中指定打印机功能条目，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* <em>功能：功能</em> 名 {<em>FeatureAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

其中，"功能名称" 是预定义的 [标准功能](standard-features.md)之一或自定义功能名称，" *FeatureAttributes* *" 是一* 组 [功能属性](feature-attributes.md)。

例如，GPD 文件可能包含以下标准 InputBin 功能规范。

```cpp
*Feature: InputBin
{
    *Name: "Paper Bin"
    *DefaultOption: Upper
    *Option: Upper
    {
        *Name: "Upper Tray"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.10
            *Cmd: "<1B>&l1H"
        }
        *Constraints: PaperSize.Env10
    }
    *Option: Manual
    {
        *Name: "Manual Feed"
        *Command: CmdSelect
        {
            *Order: DOC_SETUP.10
            *Cmd: "<1B>&l2H"
        }
        *Installable?: TRUE
    }
}
```

例如，如果重复功能规范（包括两个或多个 InputBin 功能条目），则以下规则适用：

-   未复制的属性和选项将添加到 Unidrv 的数据库中。

-   将覆盖重复的属性和选项，Unidrv 仅保留上一规范。

您可以控制向用户显示功能的顺序。 请参阅 [指定功能和选项显示顺序](specifying-feature-and-option-display-order.md)。

 

 




