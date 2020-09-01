---
title: CPSUI 支持的窗口控件
description: CPSUI 支持的窗口控件
ms.assetid: 557aa4e6-e48e-44fe-b833-93728426b056
keywords:
- 公共属性表用户界面 WDK 打印，窗口控件
- CPSUI WDK 打印，窗口控件
- 属性表页 WDK 打印，窗口控件
- 窗口控件 WDK CPSUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2316a9b3250d2e8f0e8767f9f713138c35dd597d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218258"
---
# <a name="cpsui-supported-window-controls"></a>CPSUI 支持的窗口控件





CPSUI 支持一组为用户提供一致界面的窗口控件。 在为打印机设备和文档创建属性页页面时，使用这些窗口控件尤其重要，因为用户需要为所有打印机提供一致的界面。

CPSUI 支持的窗口控件包括：

-   包含两个或三个单选按钮的框

-   滚动和跟踪栏

-   编辑框、列表框和组合框

-   向上/向下箭头框

-   复选框

指定 [属性表选项](property-sheet-options.md)时，必须始终使用这组窗口控件。 使用 [CPSUI 选项类型](./cpsui-option-types.md)指定窗口控件。 虽然通常不是必需的，但可以自定义这些控件的外观。 有关详细信息，请参阅 [自定义 CPSUI 支持的窗口控件](customizing-cpsui-supported-window-controls.md)。

CPSUI 还定义了两个称为扩展的复选框和一个扩展的 "推送" 按钮的特殊控件。 使用 EXTCHKBOX 和 EXTPUSH 结构，可以分别使用 " [**EXTCHKBOX**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_extchkbox) " 和 " [**EXTPUSH**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_extpush) " 结构来指定这些用于提供标准复选框和按钮的功能的控件。

 

