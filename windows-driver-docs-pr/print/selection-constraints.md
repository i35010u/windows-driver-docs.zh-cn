---
title: 选择约束
description: 选择约束
keywords:
- 选择约束 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5fa8d4f544778a5a4765e7c3a1eb8b2ae6dea88
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806925"
---
# <a name="selection-constraints"></a>选择约束





通常，不能同时选择各种打印机功能的某些选项。 例如，如果选择了 "信封进纸器"，则不能选择 nonenvelope 纸张大小，例如 letter 大小或 A4 大小的纸张。

若要指定不能同时选择的打印机选项组合，请使用 \* InvalidCombination 或 \* 约束项。 如果用户尝试选择指定为无效的选项组合，Unidrv 将拒绝选择。

\*InvalidCombination 条目采用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* InvalidCombination： <em>列出 ( 功能</em> 列表。 <em>OptionName</em> ，功能<em>名。</em> <em>OptionName</em> ，... ) </p></td>
</tr>
</tbody>
</table>

 

其中，"功能名称" 是功能的名称，" *OptionName* *" 是与* 该功能关联的选项的名称。

单个 InvalidCombination 条目中列出的选项 \* 指示一组不能组合使用的选项。 例如，下面的条目指定 *CMYK* 颜色模式不能与普通纸张和 720 DPI 一起使用。

```cpp
*InvalidCombination: LIST(Resolution.720dpi, MediaType.Plain, ColorMode.CMYK)
```

所有 \* InvalidCombination 条目都必须位于 GPD 文件的根级别 (即，不在大括号) 内。 条目中包含的选项数目不受限制。

如果只需要指示两个选项之间的无效组合关系，则可以使用 \* 约束项。 其格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* <em>限制：功能</em> 。 <em>OptionName</em></p></td>
</tr>
</tbody>
</table>

 

其中，"功能名称" 是功能的名称，" *OptionName* *" 是与* 该功能关联的选项的名称。 \*约束条目必须位于 \* 选项条目中。 例如，若要指示不能将 letter 大小的纸张与信封进纸器一起使用，可以使用以下条目：

```cpp
*Feature: InputBin
{
    *Option: ENVFEED
    {
        *Constraints: PaperSize.Letter
        *Constraints: PaperSize.A4
    }
}
```

或等效：

```cpp
*Feature: InputBin
{
    *Option: ENVFEED
    {
        *Constraints: LIST(PaperSize.Letter, PaperSize.A4)
    }
}
```

这些示例指定，如果用户尝试选择信封进纸器和 letter 尺寸纸张，或信封进纸器和 A4 尺寸纸张，Unidrv 将拒绝选择。

 

 




