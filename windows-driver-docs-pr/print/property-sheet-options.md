---
title: 属性表选项
description: 属性表选项
ms.assetid: 572330d6-1a1b-46fd-bfb4-be2b0990bca4
keywords:
- 公共属性表用户界面 WDK 打印，属性表选项
- CPSUI WDK 打印，属性表选项
- 属性表页 WDK 打印，属性表选项
- 属性表 WDK 打印
- 可选属性表单页面项 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcba3044edcbc629f8b7c470ed48be4b57e63fef
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207697"
---
# <a name="property-sheet-options"></a>属性表选项





属性表选项是属性表页上可显示的可选择的项。 通常，用户可以修改选项的值。 CPSUI 使用一组预定义的 [CPSUI 支持的窗口控件](cpsui-supported-window-controls.md)，帮助应用程序以标准格式创建选项。 应用程序不必为这些控件提供资源。

每个属性表页通常包含多个选项。 对于每个属性表选项，CPSUI 应用程序必须使用以下 CPSUI 结构：

-   一个 [**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 结构，用于标识选项的显示名称和其他特征。

-   一个 [**OPTTYPE**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_opttype) 结构，用于标识选项的显示对话框类型 ([CPSUI 选项类型](./cpsui-option-types.md)) 。

-   一个或多个 [**OPTPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optparam) 结构，用于标识选项的用户可选参数值。

若要使用这些 CPSUI 结构来描述属性表选项，则必须使用 [**COMPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_compropsheetui) 结构定义包含该选项的页面。

 

