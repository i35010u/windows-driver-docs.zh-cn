---
title: 创建属性表页
description: 创建属性表页
ms.assetid: 90b1743c-b530-408a-aa30-9ab774166306
keywords:
- 常用属性页用户界面 WDK 打印，创建属性表页
- CPSUI WDK 打印，创建属性表页
- 属性表页 WDK 打印创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba1a9bd3f897bcb8910653c109bfbe1a0ae512b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372431"
---
# <a name="creating-property-sheet-pages"></a>创建属性表页





使用 CPSUI 创建属性表页组成[属性工作表选项](property-sheet-options.md)，其中每个选项表示用户可修改的值。 对话框属性工作表选项是创建使用一系列[CPSUI 支持窗口控件](cpsui-supported-window-controls.md)，让用户修改选项的值。

CPSUI 提供窗口控件可以显示在[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)，或它们可以用于自定义页面。 有多个[方法来指定页面](methods-for-specifying-pages.md)，所有这些涉及调用 CPSUI 的[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)函数。

创建打印机和打印文档的属性表页涉及[CPSUI 使用打印机驱动程序](using-cpsui-with-printer-drivers.md)和需要应用程序、 打印后台处理程序、 打印机接口 DLL，以及 CPSUI 之间的交互。

 

 




