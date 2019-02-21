---
title: 功能条目格式
description: 功能条目格式
ms.assetid: f4e91611-aa68-4426-82ef-9ad3f09d62f2
keywords:
- 打印机功能 WDK Unidrv，条目格式
- 格式 WDK 打印机功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31cefd326154fe90d4a11d9e027d947f28af26db
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555181"
---
# <a name="feature-entry-format"></a>功能条目格式





若要在 GPD 文件中指定打印机功能条目，请使用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* 功能：<em>FeatureName</em> {<em>FeatureAttributes</em>}</p></td>
</tr>
</tbody>
</table>

 

其中*FeatureName*是预定义的任何一个的名称[标准功能](standard-features.md)或自定义的功能名称，并*FeatureAttributes*是一套[功能属性](feature-attributes.md)。

例如，GPD 文件可能包含以下标准版 InputBin 功能规范。

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

如果重复的功能规范，例如，包括两个或多个 InputBin 功能条目，则适用以下规则：

-   属性和不重复的选项添加到 Unidrv 的数据库中。

-   属性和重复的选项将被覆盖，并 Unidrv 保留仅最新的规范。

您可以控制向用户显示功能的顺序。 请参阅[指定的功能和选项显示顺序](specifying-feature-and-option-display-order.md)。

 

 




