---
title: 控制图像质量
description: 控制图像质量
keywords:
- Unidrv，图像质量
- 图像质量选项 WDK Unidrv
- 草稿图像质量 WDK Unidrv
- 更好的图像质量 WDK Unidrv
- 最佳图像质量 WDK Unidrv
- 质量设置项 WDK Unidrv
- 打印作业 WDK，图像质量
- 格式化 WDK 图像质量
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9caf7e8fe4d7de5270d8a35b389eab0353ede9e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797535"
---
# <a name="controlling-image-quality"></a>控制图像质量





Unidrv 的用户界面提供一组三个单选按钮，允许用户选择 "草稿"、"更好" 或 "最佳" 图像质量来打印作业。 草稿质量强调打印机在图像分辨率上的速度，而最佳质量则会相反。

这些单选按钮的用途是使用户可以轻松地选择获取所需质量所需的功能选项，而无需单独显式选择所需的选项。

按下某个单选按钮时，Unidrv 应选择的选项在打印机的 GPD 文件中指定。 GPD 语言定义以下三个条目：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><em><strong>DraftQualitySettings</strong></p></td>
</tr>
<tr class="even">
<td><p></em><strong>BetterQualitySettings</strong></p></td>
</tr>
<tr class="odd">
<td><p>*<strong>BestQualitySettings</strong></p></td>
</tr>
</tbody>
</table>

 

其中的每个条目都与某个单选按钮相关联，并且每个条目都接受一个选项列表。 当用户选择相应的按钮时，Unidrv 将遍历列表并设置指定的选项。

每个质量设置条目的格式如下所示：

\**XXXX* QualitySettings：*列出 (功能* 列表。*OptionName*，功能 *名。**OptionName*，功能 *名。**OptionName*，... ) 

*其中每个* 功能名称是与功能条目关联的名称 \* *Feature* ， *OptionName* 是与该功能的一个 \* *选项* 条目关联的名称。 空列表导致关联的单选按钮灰显。

附加的必需条目指定默认图像质量。 其格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>DefaultQuality：</strong> <em>DefaultQuality</em></p></td>
</tr>
</tbody>
</table>

 

其中， *DefaultQuality* 是 `DRAFTQUALITY` 、或之一 `BETTERQUALITY` `BESTQUALITY` 。

这些 GPD 文件项可以与和功能的任何选项关联 `ColorMode` `MediaType` 。 通常，它们放置在 [条件语句](conditional-statements.md)中，如下面的示例中所示。

```cpp
*switch: ColorMode {
    *case: Mono {
        *BestQualitySettings: LIST(ColorMode.Mono,
                                   Resolution.Option1,
                                   TextQuality.Option3)
        *BetterQualitySettings: LIST(ColorMode.Mono,
                                     Resolution.Option1,
                                     TextQuality.Option1)
        *DraftQualitySettings: LIST(ColorMode.Mono,
                                    Resolution.Option2,
                                    TextQuality.Option2)
        *DefaultQuality: BETTERQUALITY }
    *default: {
        *BestQualitySettings: LIST(ColorMode.24bpp,
                                   Resolution.Option2,
                                   TextQuality.Option3)
        *BetterQualitySettings: LIST(ColorMode.Color,
                                     Resolution.Option2,
                                     TextQuality.Option1)
        *DraftQualitySettings: LIST(ColorMode.Color,
                                    Resolution.Option2,
                                    TextQuality.Option2)
        *DefaultQuality: BETTERQUALITY }}
```

如示例中所示，一个好的策略是为 \* 单颜色模式指定一个 **事例** 条目，然后 \* 对所有多色模式使用 *_默认_* 条目。 这是因为，Unidrv 的 " **页面设置** " 属性页页面为用户提供了两种选择：彩色打印或 noncolor 打印。 如果使用示例中的格式，则当用户选择颜色打印选项时，Unidrv 将显示质量按钮。

下面是一个更复杂的示例，该示例将图像质量与彩色模式和媒体类型紧密结合：

```cpp
*switch: Colormode {
    *case: Mono {
    *switch: MediaType {
        *case: CLAYCOATED {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BESTQUALITY }
        *case: GLOSSY {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BETTERQUALITY 
        *default: 
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  DRAFTQUALITY }}}
    *default: {
    *switch: MediaType {
        *case: CLAYCOATED {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BESTQUALITY }
        *case: GLOSSY {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  BETTERQUALITY }
        *default: {
            *DraftQualitySettings:  LIST(Option List)
            *BetterQualitySettings:  LIST(Option List)
            *BestQualitySettings:  LIST(Option List)
            *DefaultQuality:  DRAFTQUALITY }}}
}
```

使用 quality 设置 GPD 项时，必须遵守以下规则：

-   必须始终使用全部四个条目。 允许指定空选项列表，并使关联的单选按钮灰显。

-   必须为所有 ColorMode 和媒体的组合指定所有四个条目。 示例使用 \* 每个条件语句中的 **默认** 项来实现此目的。

-   质量设置项中的选项列表不得违反指定的任何 [选项约束](option-constraints.md) 。

-   选项列表中包含的选项不应更改所选的媒体类型。 同时，虽然可接受，但要将颜色模式设置为24位/像素以获得最佳质量，为8位/像素设置为更高的质量，将4位/像素更改为1个比特/像素 (单色) 不可接受。

如果在指定质量设置的条件语句中包含功能，则分析器将该功能的 \* UpdateQualityMacro？特性设置为 **TRUE**。  (参阅 [功能特性](feature-attributes.md)。 ) 

 

 




