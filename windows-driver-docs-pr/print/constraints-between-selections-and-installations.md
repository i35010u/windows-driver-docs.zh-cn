---
title: 选择与安装之间的约束
description: 选择与安装之间的约束
ms.assetid: abb6004f-daae-4f28-b36c-102d0b8c9f55
keywords:
- 安装 WDK Unidrv 约束
- 选择约束 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e09254f2efed71de895b90b2393deeece3761e2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383162"
---
# <a name="constraints-between-selections-and-installations"></a>选择与安装之间的约束





有时有必要指定如果安装一些其他选项，则不能选择某个选项，或如果未安装一些其他选项，则不能选择某个选项。 例如，用户不应能够选择 tabloid 纸，如果未安装打印机的大画幅送纸器。

若要指定某些选项与其他选项的安装状态的选择之间的关系，请使用\* **InstalledConstraints**并\* **NotInstalledConstraints**条目。 其格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>InstalledConstraints:<em>FeatureName</em> 。 <em>OptionName</em></p></td>
</tr>
<tr class="even">
<td><p></em>NotInstalledConstraints:<em>FeatureName</em> 。 <em>OptionName</em></p></td>
</tr>
</tbody>
</table>

 

其中*FeatureName*是一项功能的名称和*OptionName*与功能相关联的选项的名称。 如果参数是一项功能，段和*OptionName*不包括在内。

\* **InstalledConstraints**或\* **NotInstalledConstraints**条目必须位于内部\*功能或\*选项条目。 例如，若要指示用户不应能够选择 tabloid 纸，如果未安装打印机的大画幅送纸器，可以使用以下项：

```cpp
*Feature: InputBin
{
    *Option: LARGEFMT
    {
        Installable?: TRUE
        NotInstalledConstraints: PaperSize.TABLOID
    }
}
```

如果某项功能或选项包括\* **InstalledConstraints**或\* **NotInstalledConstraints**条目、 功能或选项的\*可安装？ 属性必须设置为 **，则返回 TRUE**。

 

 




