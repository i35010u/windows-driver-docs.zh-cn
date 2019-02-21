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
ms.openlocfilehash: 9f42f5ff37f80e68a03aa2debae38b5be43f0cae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526647"
---
# <a name="creating-property-sheet-pages"></a>创建属性表页





使用 CPSUI 创建属性表页组成[属性工作表选项](property-sheet-options.md)，其中每个选项表示用户可修改的值。 对话框属性工作表选项是创建使用一系列[CPSUI 支持窗口控件](cpsui-supported-window-controls.md)，让用户修改选项的值。

CPSUI 提供窗口控件可以显示在[CPSUI 提供页和模板](cpsui-supplied-pages-and-templates.md)，或它们可以用于自定义页面。 有多个[方法来指定页面](methods-for-specifying-pages.md)，所有这些涉及调用 CPSUI 的[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)函数。

创建打印机和打印文档的属性表页涉及[CPSUI 使用打印机驱动程序](using-cpsui-with-printer-drivers.md)和需要应用程序、 打印后台处理程序、 打印机接口 DLL，以及 CPSUI 之间的交互。

 

 




