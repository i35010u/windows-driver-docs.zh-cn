---
title: CPSUI 支持窗口控件
description: CPSUI 支持窗口控件
ms.assetid: 557aa4e6-e48e-44fe-b833-93728426b056
keywords:
- 常用属性页用户界面 WDK 打印，窗口控件
- CPSUI WDK 打印，窗口控件
- 属性表页 WDK 打印，窗口控件
- 窗口控件 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 701bc284d746eaf7e81991bbf94ed4dbade64622
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555236"
---
# <a name="cpsui-supported-window-controls"></a>CPSUI 支持窗口控件





CPSUI 支持一组向用户提供了一致的界面的窗口控件。 这些窗口控件的使用是特别重要创建时属性表页为打印机设备和文档，因为用户希望所有打印机的一致界面。

CPSUI 支持窗口控件包括：

-   包含两个或三个单选按钮的框

-   滚动和跟踪条

-   编辑、 列表中，和组合框

-   向上/向下箭头框

-   复选框

指定时，始终必须使用此组窗口控件[属性工作表选项](property-sheet-options.md)。 使用指定的窗口控件[CPSUI 选项类型](https://msdn.microsoft.com/library/windows/hardware/ff547142)。 虽然通常这不是必需的可以自定义这些控件的外观。 有关详细信息，请参阅[Customizing CPSUI-Supported 窗口控件](customizing-cpsui-supported-window-controls.md)。

CPSUI 还定义了两个特殊控件，调用扩展的复选框和扩展的推送按钮。 这些控件，它们提供超出标准复选框和推送按钮的功能，可以使用指定[ **EXTCHKBOX** ](https://msdn.microsoft.com/library/windows/hardware/ff548781)并[ **EXTPUSH**](https://msdn.microsoft.com/library/windows/hardware/ff548795)结构，分别。

 

 




