---
title: 选择与安装之间的约束
description: 选择与安装之间的约束
keywords:
- 安装约束 WDK Unidrv
- 选择约束 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b5e3530c92297740d2952cc441ec2804afbcade
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797557"
---
# <a name="constraints-between-selections-and-installations"></a>选择与安装之间的约束





有时，需要指定在安装其他某个选项时无法选择某个选项，或者，如果未安装某个其他选项，则无法选择某个选项。 例如，如果未安装打印机的大格式纸盒，则用户不能选择 "tabloid 纸"。

若要指定特定选项与其他选项的安装状态之间的关系，请使用 \* **InstalledConstraints** 和 \* *_NotInstalledConstraints_* 项。 其格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em>InstalledConstraints： <em>功能</em> 名。 <em>OptionName</em></p></td>
</tr>
<tr class="even">
<td><p></em>NotInstalledConstraints： <em>功能</em> 名。 <em>OptionName</em></p></td>
</tr>
</tbody>
</table>

 

其中，"功能名称" 是功能的名称，" *OptionName* *" 是与* 该功能关联的选项的名称。 如果参数是一项功能，则不包含句点和 *OptionName* 。

\*必须将 **InstalledConstraints** 或 \* *_NotInstalledConstraints_* 条目放入 \* 功能或 \* 选项条目中。 例如，若要指示如果未安装打印机的大格式纸盒，用户不能选择 "tabloid 纸"，可以使用以下条目：

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

如果功能或选项包含 \* **InstalledConstraints** 或 \* *_NotInstalledConstraints_* 条目，则功能或选项的 "可 \* 安装？" 属性必须设置为 **TRUE**。

 

 




