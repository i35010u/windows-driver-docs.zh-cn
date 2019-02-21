---
title: 自定义 CPSUI 支持窗口控件
description: 自定义 CPSUI 支持窗口控件
ms.assetid: b9ced902-6368-4b3b-a974-81e7d38c0ced
keywords:
- 常用属性页用户界面 WDK 打印，窗口控件
- CPSUI WDK 打印，窗口控件
- 属性表页 WDK 打印，窗口控件
- 窗口控件 WDK CPSUI
- 自定义 CPSUI 支持窗口控件 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c21e159da744343971dec67a4d3fcc104bd50c7
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555243"
---
# <a name="customizing-cpsui-supported-window-controls"></a>自定义 CPSUI 支持窗口控件





如果使用的[CPSUI 支持窗口控件](cpsui-supported-window-controls.md)结合[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)，CPSUI 提供介绍允许的方式的控件的窗口中控制资源它们组合在一起。 因此，不需要为控件提供资源。

但是，如果要创建不使用 CPSUI 提供页面或模板的属性表页，您必须自定义使用 CPSUI 支持窗口控件。 若要执行此操作，需要提供的窗口中控制资源[CPSUI 选项类型](https://msdn.microsoft.com/library/windows/hardware/ff547142)。 必须指定使用这些资源的标识符**BegCtrlID**成员的每个选项[ **OPTTYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff559670)结构。

如果要自定义 CPSUI 支持窗口控件，请记住 CPSUI 不会显示一个选项，如果 OPTIF\_中设置隐藏标志[ **OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)结构。 CPSUI 移动剩余的控件来填充通常由隐藏选项占用的空间。 因此，如果要创建一个包含多个同时显示选项的页面，则应遵守以下规则：

-   每个选项应占用属性表页的整个水平空间。

-   选项对话框不应覆盖彼此。

-   有关从左到右排列的单选按钮所表示的选项，应在 x 轴上对齐按钮和图标。 如果按钮从上到下排列，应在 y 轴上对齐按钮和图标。

-   如果多个项共享一组框中，必须属于组框中的第一个[ **OPTITEM**](https://msdn.microsoft.com/library/windows/hardware/ff559656)，这是在组中最顶层的项。 分组框必须足够大以包含与之关联的所有项。

另请注意，如果从上到下和某些控制处于隐藏状态排列的单选按钮和图标，CPSUI 不会删除生成的空白区域在 y 方向。

 

 




