---
title: 条件语句
description: 条件语句
keywords:
- Unidrv，条件语句
- GPD 文件 WDK Unidrv，条件语句
- 条件语句 WDK Unidrv
- 多个依赖项 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 113869a5c607c0be27fa71f59f2321e10fe6cde4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797597"
---
# <a name="conditional-statements"></a>条件语句





GPD 语言提供了类似于 C 的条件语句，使你可以描述某些打印机属性可对打印机配置具有的依赖项。 例如，页面的边距和光标原点可能取决于页面的方向。 **\* Switch** 和 **\* Case** 语句允许您表达此类依赖项。 这些语句的格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p>
* Switch <em>功能</em> 名 {* case <em>Option1_Name</em> {} * case <em>Option2_Name</em> {} <em>等</em> <em>OptionN_Name</em> {} * 默认值 {}}</td>
</tr>
</tbody>
</table>

 

功能 *名称必须是* 包含 **\* 功能** 条目的 GPD 文件中指定的功能的名称。 使用的选项名称必须是与指定功能相关联的选项。

若要表达页边距和光标源依赖于页面方向的情况，可以使用以下条目：

```cpp
*Feature: Orientation
{
    *DefaultOption: Portrait
    *Option: Portrait
    {
        *Name: "Portrait"
        *rcIconID: =RC_ICON_PORTRAIT
    }
    *Option: LANDSCAPE_CC90
    {
        *Name: "Landscape"
        *rcIconID: =RC_ICON_LANDSCAPE
    }
}
*Feature: PaperSize
{
    *DefaultOption: Letter
    *Option: Letter
    {
        *Name: "Letter 8.5 x 11 inch"
        *switch: Orientation
        {
            *case: Portrait
            {
                *PrintableArea: PAIR(4800, 6324)
                *PrintableOrigin: PAIR(150, 150)
                *CursorOrigin: PAIR(150,100)
            }
            *case: LANDSCAPE_CC90
            {
                *PrintableArea: PAIR(4860, 6360)
                *PrintableOrigin: PAIR(120, 120)
                *CursorOrigin: PAIR(100,6480)
            }
        }
    }
}
```

在此示例中，打印机的 **PaperSize** 功能的选项取决于打印机 **方向** 功能的所选选项。

如果没有将功能的所有选项列出为 **\* Case** 语句参数，则可以包含 **\* 默认** 语句，就像 C 语言中一样。 如果未包括所有选项，并且未包括 **\* 默认** 语句，则必须在 PrintableArea、PrintableOrigin 和 CursorOrigin 中的 **\***、 \* *_PrintableOrigin_* 和) **\*** 中计算相关属性 (，在 \* *_Switch_* 语句前面。

### <a name="specifying-multiple-dependencies"></a><a href="" id="ddk-specifying-multiple-dependencies-gg"></a>指定多个依赖项

可以在 **\* Case** 和 **\* Default** 语句中包含 **\* Switch** 语句。 这允许您指定多个依赖项，如下所示：

```cpp
*Feature: feature1 {*Option: optionA {...} *Option: optionB {...}}
*Feature: feature2 {*Option: optionC {...} *Option: optionD {...}}
*Feature: feature3 
    {*Option: optionE 
        {*Switch: feature1 
            {*Case: optionA
                 {*Switch: feature2
                     {*Case: optionD
                         {AttributeX: ValueX}
                      *Default
                         {AttributeX: ValueY}
                     }
                 }
             *Default
                  {AttributeX: ValueZ}
             }
         }
    *Option: optionF {...} 
    }
```

在此示例中，AttributeX 是 feature3 的 optionE，同时依赖于 feature1 和 feature2。

如果用户已选择 optionA for feature1，optionD for feature2，optionE feature3，则 attributeX 设置为 ValueX。

如果用户已选择 optionA for feature1，optionC for feature2，optionE feature3，则 attributeX 设置为 ValueY。

如果用户已选择 optionB for feature1，optionE 为 feature3，则 attributeX 设置为 ValueZ。 Feature2 的设置不相关。

指定多个依赖项时，下列规则适用：

-   必须在单个 **\* 交换机** 条目的作用域内指定多个依赖项。 例如，使用示例，你不能使用 **\* 开关** 项来指示 feature3 依赖于 feature1，然后在后续的非嵌套 **\* Switch** 语句中，指示 feature3 依赖于 feature2。

-   不能在每个嵌套交换机条目中多次指定相同的功能 \* *_Switch_* 。

### <a name="where-to-place-a-switch-statement"></a><a href="" id="ddk-where-to-place-a-switch-statement-gg"></a>Switch 语句的放置位置 \*

可以在 GPD 文件中的以下位置放置 **\* Switch** 语句：

-   在 \* 选项语句中

-   在 \* 功能语句内

-   在 **\* Case** 语句内

-   在 **\* 默认** 语句中

-   在文件的顶层 (即，不在一组大括号内) 

### <a name="what-to-place-inside-switch-case-and-default-statements"></a><a href="" id="ddk-what-to-place-inside-switch-case-and-default-statements-gg"></a>\*Switch、 \* Case 和 \* Default 语句中要放置的内容

在 **\* 交换机** 条目中，只能放置 **\* Case** 和 **\* Default** 条目。

可放置在 **\* Case** 或 **\* 默认** 项内的 GPD 文件项称为可重定位项。 以下类型的 GPD 项可重定位：

-   大多数 [打印机属性](printer-attributes.md)（ [仅限根级别属性](root-level-only-attributes.md)除外）。  ([常规属性](general-attributes.md)前面必须是 EXTERN \_ GLOBAL，除非 \* *_交换机_* 条目位于根级别（不在大括号内）。 ) 

-   嵌套式 \* *_交换机_* 条目，可用于指定多个依赖关系。

-   \*命令条目。

-   \*TTFSEnabled？，用于实现字体替换。

以下类型的 GPD 项不可重定位：

-   仅限根级别的特性。

-   \*用于指定替换字体的 TTFS 项。

-   \*约束、 \* InvalidCombination、 \* InvalidInstallableCombination、 \* NotInstalledConstraints 项定义了无效的选项组合，如 [选项约束](option-constraints.md)中所述。

-   \*功能和 \* 选项项 (虽然 [功能特性](feature-attributes.md) 和 [选项特性](option-attributes.md) 可) 重定位。

确定是否已正确地在 Case 语句中放置项的一种方法 \* **Case** 是删除所有 \* *_Switch_* 和 \* *_Case_* 语句。 如果 \* *_Case_* 语句内的条目是正确的，则在 \* 删除 *_Switch_* 和 \* *_Case_* 语句后，它们仍然是正确的。

### <a name="ordering-of-switch-statements-in-a-v4-print-driver-derived-from-a-class-driver"></a>V4 打印驱动程序中从类驱动程序派生的 switch 语句排序

派生的 v4 打印机驱动程序的 GPD 文件需要遵循与基类驱动程序相同的顺序。

请考虑以下场景。 通过将 **RequiredClass** 设置为-manifest.ini 文件中的类驱动程序，可以从 v4 类驱动程序派生 v4 打印机驱动程序 \* 。

类驱动程序的 GPD 文件具有以下开关树：

```cpp
* Option: A4
    1. Switch: Resolution
* Option: Letter
    1. Switch: Resolution
    2. Switch: InputBin
```

派生的 v4 打印机驱动程序想要添加 **MarginSetting** 开关，因此其 GPD 文件将具有以下开关树：

```cpp
* Option: A4
    1. Switch: Resolution
    2. Switch: InputBin
    3. Switch: MarginSetting
* Option: Letter
    1. Switch: Resolution
    2. Switch: InputBin
    3. Switch: MarginSetting
```

请注意， **解析** 在派生的 GPD 中的 **InputBin** 之前设置，而 **MarginSetting** 在这两个之后设置。 派生的 v4 打印机驱动程序的 GPD 文件的顺序与基类驱动程序的相同，并在之后添加 **MarginSetting** 。

例如，错误派生的 GPD 文件可能如下所示：

```cpp
* Option: A4
    1. Switch: MarginSetting
    2. Switch: InputBin
    3. Switch: Resolution
* Option: Letter
    1. Switch: MarginSetting
    2. Switch: InputBin
    3. Switch: Resolution
```

 

 




