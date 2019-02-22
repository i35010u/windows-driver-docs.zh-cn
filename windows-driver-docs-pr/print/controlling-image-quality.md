---
title: 控制图像质量
description: 控制图像质量
ms.assetid: b6d25178-6726-4ce0-ab34-efeedc618044
keywords:
- Unidrv，图像质量
- 图像质量选项 WDK Unidrv
- 草稿图像质量 WDK Unidrv
- 更好的图像质量 WDK Unidrv
- 最佳图像质量 WDK Unidrv
- 质量设置条目 WDK Unidrv
- 打印作业 WDK，图像质量
- 格式 WDK 图像质量
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5f993d6dc41c93c245993e2b1c841a00480dd9d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519253"
---
# <a name="controlling-image-quality"></a>控制图像质量





Unidrv 的用户界面提供一组三个单选按钮，允许用户选择"草稿"，"更好"或"最好"图像质量的打印作业。 草稿质量最佳质量执行相反的操作时，通过图像分辨率高低，强调打印机速度。

这些单选按钮的用途是允许用户能够轻松选择所需获取所需的质量，并且无需单独显式选择所需的选项的功能选项。

打印机的 GPD 文件中指定的单选按钮被按下时，应选择 Unidrv 的选项。 GPD 语言定义以下三项：

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

 

每个条目与其中一个单选按钮关联，每个条目接受选项的列表。 当用户选择相应的按钮时，Unidrv 列表，并设置指定的选项。

为每个质量设置条目的格式如下所示：

\**XXXX*QualitySettings:列表 (*FeatureName*。*OptionName*， *FeatureName*。*OptionName*， *FeatureName*。*选项名称*，...)

其中每个*FeatureName*一个名称与相关联\**功能*条目，和*OptionName*是一个名称与关联的功能之一的\**选项*条目。 一个空列表会导致该相关联的单选按钮灰显。

附加的所需条目指定的默认图像质量。 格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>*<strong>DefaultQuality:</strong><em>DefaultQuality</em></p></td>
</tr>
</tbody>
</table>

 

其中*DefaultQuality*是之一`DRAFTQUALITY`， `BETTERQUALITY`，或`BESTQUALITY`。

这些 GPD 文件条目可以使用的任何选项相关联`ColorMode`和`MediaType`功能。 通常情况下，它们都将置于[条件语句](conditional-statements.md)，如以下示例所示。

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

在示例中所示，一个好的策略是指定一个\***用例**条目为单色模式，然后使用\***默认**所有多色模式下的条目。 这是因为 Unidrv 的**页面设置**属性表页向用户提供了两个选择-颜色或普通打印。 如果在示例中使用格式，Unidrv 显示质量按钮时用户选择颜色打印选项。

下面是更复杂示例，这会为这两种颜色模式的图像质量和媒体类型：

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

当使用质量设置 GPD 条目时，必须遵守以下规则：

-   必须始终使用所有四个条目。 指定空的选项列表允许，并且会导致该相关联的单选按钮灰显。

-   必须指定所有 ColorMode 和媒体类型组合的所有四个条目。 这些示例使用\***默认**中每个条件语句，以实现此目的的条目。

-   质量设置条目中的选项列表不能违反任何[选项约束](option-constraints.md)已指定。

-   包含在选项列表中的选项不应更改所选的介质类型。 此外，可接受时，例如，若要设置为 24 位/像素的最佳质量、 质量更好的 8 位/像素的颜色模式和 4 草稿品质，更改为 1 位/像素 （单色） 为每像素位将无法接受。

如果一项功能包含在指定质量设置的条件语句，分析器设置的功能\*UpdateQualityMacro？ 归于**TRUE**。 (请参阅[功能特性](feature-attributes.md)。)

 

 




