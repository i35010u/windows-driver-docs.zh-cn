---
title: 选择约束
description: 选择约束
ms.assetid: 9537e4c7-2cee-494d-b1ec-95d8c91a90e6
keywords:
- 选择约束 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 77b8d32a741abb4770b9dc935a1d6775210ba9fb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564448"
---
# <a name="selection-constraints"></a>选择约束





通常情况下，不能同时选择各种打印机功能的某些选项。 例如，如果选择了信封进纸器，然后 nonenvelope 纸张大小，例如信纸尺寸或 A4 大小的纸张，无法选择。

若要指定不能同时选择的打印机选项的组合，请使用\*InvalidCombination 或\*约束条目。 如果用户尝试选择已指定为无效的选项的组合，Unidrv 会拒绝所选内容。

\*InvalidCombination 条目采用以下格式：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* InvalidCombination:列表 ( <em>FeatureName</em> 。 <em>OptionName</em> ， <em>FeatureName</em> 。 <em>选项名称</em>，...)</p></td>
</tr>
</tbody>
</table>

 

其中*FeatureName*是一项功能的名称和*OptionName*与功能相关联的选项的名称。

在单个列出的选项\*InvalidCombination 条目指示一组不能结合使用的选项。 例如，以下条目规定*CMYK*颜色模式不能用于普通纸和 720 DPI。

```cpp
*InvalidCombination: LIST(Resolution.720dpi, MediaType.Plain, ColorMode.CMYK)
```

所有\*InvalidCombination 条目必须位于 GPD 文件的根级别 (即，不在大括号内)。 项中包含的选项数不受限制。

如果您只需指示两个选项之间的组合无效关系，则可以使用\*约束条目。 其格式为：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>* 约束：<em>FeatureName</em> 。 <em>OptionName</em></p></td>
</tr>
</tbody>
</table>

 

其中*FeatureName*是一项功能的名称和*OptionName*与功能相关联的选项的名称。 一个\*约束条目必须位于内部\*选项条目。 例如，若要指示信纸尺寸和 A4 大小的纸张不能用于信封进纸器，可以使用以下项：

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

或者，也可以说：

```cpp
*Feature: InputBin
{
    *Option: ENVFEED
    {
        *Constraints: LIST(PaperSize.Letter, PaperSize.A4)
    }
}
```

这些示例指定是否用户尝试选择信封进纸器和信纸尺寸的纸张或信封进纸器和 A4 大小的纸张，Unidrv 拒绝所选内容。

 

 




