---
title: 自定义 CPSUI 支持的窗口控件
description: 自定义 CPSUI 支持的窗口控件
ms.assetid: b9ced902-6368-4b3b-a974-81e7d38c0ced
keywords:
- 公共属性表用户界面 WDK 打印，窗口控件
- CPSUI WDK 打印，窗口控件
- 属性表页 WDK 打印，窗口控件
- 窗口控件 WDK CPSUI
- 自定义 CPSUI 支持的窗口控件 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04c5b4ae7250adcc786299abcb6a7a3f8b58eac9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218244"
---
# <a name="customizing-cpsui-supported-window-controls"></a>自定义 CPSUI 支持的窗口控件





如果你将 [CPSUI 支持的窗口控件](cpsui-supported-window-controls.md) 与 [CPSUI 提供的页和模板](cpsui-supplied-pages-and-templates.md)结合使用，则 CPSUI 提供了窗口控件资源，这些资源将以允许它们组合在一起的方式描述控件。 因此，不需要为控件提供资源。

另一方面，如果要创建的属性表页不使用 CPSUI 提供的页或模板，则必须自定义所使用的 CPSUI 支持的窗口控件。 为此，需要提供 [CPSUI 选项类型](./cpsui-option-types.md)的窗口控件资源。 必须使用每个选项的[**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype)结构的**BegCtrlID**成员指定这些资源的标识符。

如果要自定义 CPSUI 支持的窗口控件，请记住，如果在 \_ [**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 结构中设置了 OPTIF HIDE 标志，则 CPSUI 不会显示选项。 CPSUI 将剩余的控件移到隐藏选项通常占用的空间。 因此，如果要创建包含多个同时显示的选项的页面，应服从以下规则：

-   每个选项都应占用属性表页的整个水平空间。

-   选项对话框不应相互重叠。

-   对于按从左到右排列的单选按钮表示的选项，应在 x 轴上对齐按钮和图标。 如果按钮按从上到下排列，则按钮和图标应在 y 轴上对齐。

-   如果有多个项共享一个组框，则组框必须属于第一个 [**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)，这是分组框中最顶层的项。 分组框必须足够大才能包含所有关联项。

另请注意，如果单选按钮和图标从上到下排列，其中一些控件处于隐藏状态，则 CPSUI 不会删除 y 方向产生的空白区域。

 

