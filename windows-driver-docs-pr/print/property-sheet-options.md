---
title: 属性表选项
description: 属性表选项
ms.assetid: 572330d6-1a1b-46fd-bfb4-be2b0990bca4
keywords:
- 常用属性页用户界面 WDK 打印，属性表选项
- CPSUI WDK 打印，属性表选项
- 属性表页 WDK 打印，属性表选项
- 属性表 WDK 打印
- 可选择属性表页项 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c3daf9f4a1554970fcaa231028ebdd9f6a06af9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356022"
---
# <a name="property-sheet-options"></a>属性表选项





属性表选项是在属性表页上的可显示，可选择项。 通常情况下，用户可以修改选项的值。 CPSUI 有助于采用标准格式，创建选项的应用程序使用一组预定义的[CPSUI 支持窗口控件](cpsui-supported-window-controls.md)。 应用程序无需为这些控件提供资源。

每个属性表页通常包含多个选项。 对于每个属性表选项，CPSUI 应用程序必须使用以下 CPSUI 结构：

-   一个[ **OPTITEM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optitem)结构，它标识选项的显示名称和其他特征。

-   一个[ **OPTTYPE** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_opttype)结构，它标识的选项显示对话框类型 ([CPSUI 选项类型](https://docs.microsoft.com/windows-hardware/drivers/print/cpsui-option-types))。

-   一个或多个[ **OPTPARAM** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_optparam)结构，它识别的选项可供用户选择参数值。

若要使用这些 CPSUI 结构来描述属性工作表选项，包含选项的页必须使用定义[ **COMPROPSHEETUI** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_compropsheetui)结构。

 

 




