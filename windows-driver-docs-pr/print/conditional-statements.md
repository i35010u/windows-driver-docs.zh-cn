---
title: 条件语句
description: 条件语句
ms.assetid: eea2f9c1-a73b-46ed-a778-ece6bed615ac
keywords:
- Unidrv，条件语句
- GPD 文件 WDK Unidrv，条件语句
- 条件语句 WDK Unidrv
- 多个依赖项 WDK Unidrv
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f2476cf2a96ea99b5a07a41c72a5eb16379b0c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546989"
---
# <a name="conditional-statements"></a>条件语句





GPD 语言提供了类似于 C 的条件语句，可用于描述某些打印机属性可以使用打印机的配置的依赖关系。 例如，边距和页的游标来源可能取决于页面方向。 **\*交换机**并**\*用例**语句允许您表示此类依赖项。 这些语句的格式如下所示：

<table>
<colgroup>
<col width="100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p>
* 切换<em>FeatureName</em> {* 用例<em>Option1_Name</em> {} * 用例<em>Option2_Name</em> {}<em>等</em>* 用例<em>OptionN_Name</em>{} * 默认 {}}</td>
</tr>
</tbody>
</table>

 

*FeatureName*必须是一项功能，GPD 文件中指定的名称**\*功能**条目。 使用的选项名称必须与指定的功能相关联的选项。

要表示边距和游标来源都依赖于页面方向在哪一页中，可以使用以下项：

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

在此示例中，相应的选项的打印机**PaperSize**功能都依赖于所选的选项的打印机**方向**功能。

如果未列出的所有功能的选项作为**\*用例**语句参数，可以包括**\*默认**语句，就像 C 语言中一样。 如果不包括所有选项，并且不都包括**\*默认**语句，则必须评估相关属性 (在示例中，  **\*PrintableArea**， \* **PrintableOrigin**，并 **\*CursorOrigin**) 前面的 GPD 文件中的其他位置\***交换机**语句。

### <a href="" id="ddk-specifying-multiple-dependencies-gg"></a>指定多个依赖项

可以包括**\*交换机**内的语句**\*用例**并**\*默认**语句。 这可以指定多个依赖项，按如下所示：

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

在此示例中 AttributeX，属于 optionE feature3，是依赖于 feature1 和功能 2。

如果用户已选定 feature1 的以及可选、 功能 2，为 optionD feature3 的 optionE，然后 attributeX 设置为值 x。

如果用户已选定 feature1 的以及可选、 功能 2，为 optionC feature3 的 optionE，然后 attributeX 设置为 ValueY。

如果用户已选定为 feature1 optionB 和 feature3 的 optionE，然后 attributeX 设置为 ValueZ。 功能 2 的设置无关。

指定多个依赖项时，将应用以下规则：

-   多个依赖项必须指定一个作用域内**\*交换机**条目。 使用示例，例如，您不能使用**\*交换机**条目，以指示该 feature3 是依赖 feature1，然后，在后续非嵌套**\*开关**语句中，指示该 feature3 是依赖于功能 2。

-   您不能多次指定相同的功能中每个嵌套\***交换机**条目。

### <a href="" id="ddk-where-to-place-a-switch-statement-gg"></a>下一位置\*Switch 语句

可以将放置**\*交换机**GPD 文件中的以下位置中的语句：

-   内部\*选项语句

-   内部\*功能语句

-   内部**\*用例**语句

-   内部**\*默认**语句

-   在该文件的顶部级别 (即，而不是在一组大括号)

### <a href="" id="ddk-what-to-place-inside-switch-case-and-default-statements-gg"></a>内发生的内容\*开关，\*的情况下，和\*默认语句

内**\*交换机**条目，然后就可以仅**\*用例**并**\*默认**条目。

可以放置在的 GPD 文件条目**\*用例**或**\*默认**条目被称为可重定位项。 可重定位是以下类型的 GPD 条目：

-   大多数[打印机属性](printer-attributes.md)，除[仅限根级别属性](root-level-only-attributes.md)。 ([常规属性](general-attributes.md)前面必须是外部\_GLOBAL 除非\***开关**条目是在根级别-不在大括号内。)

-   嵌套\***交换机**，可以指定多个依赖项的条目。

-   \*命令项。

-   \*TTFSEnabled？，可让字体替换。

以下类型的 GPD 条目不是可重定位的：

-   仅在根级别的特性。

-   \*用于指定 TTFS 条目替换字体。

-   \*约束\*InvalidCombination， \*InvalidInstallableCombination，\*中所述定义无效的选项，组合的 NotInstalledConstraints 条目[选项约束](option-constraints.md).

-   \*功能和\*选项的条目 (尽管[功能特性](feature-attributes.md)并[选项属性](option-attributes.md)是可重定位)。

一种方法可以确定是否条目置于正确地深入了解\***用例**语句将删除所有\***开关**并\***用例**语句。 如果中的条目\***用例**陈述是正确的它们是否仍正确后\***开关**并\***用例**删除语句。

### <a name="ordering-of-switch-statements-in-a-v4-print-driver-derived-from-a-class-driver"></a>V4 打印驱动程序派生自类驱动程序中的 switch 语句的顺序

派生的 v4 打印机驱动程序 GPD 文件需要遵循的基本类驱动程序的顺序相同。

请考虑以下方案。 必须通过设置派生自 v4 类驱动程序的 v4 打印机驱动程序**RequiredClass**中的类驱动程序到\*-manifest.ini 文件。

类驱动程序 GPD 文件具有以下开关树：

```cpp
* Option: A4
    1. Switch: Resolution
* Option: Letter
    1. Switch: Resolution
    2. Switch: InputBin
```

派生的 v4 打印机驱动程序想要添加**MarginSetting**切换，因此其 GPD 文件包含以下开关树：

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

请注意，**解析**之前设置**InputBin**中派生 GPD 并**MarginSetting**后两者设置。 派生的 v4 打印机驱动程序 GPD 文件遵循的基本类驱动程序的顺序相同，并将添加**MarginSetting**后。

例如，错误地派生的 GPD 文件可能如下所示：

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

 

 




