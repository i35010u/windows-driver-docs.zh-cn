---
title: 父级组
description: 父级组
ms.assetid: b4c40c15-df16-4af0-81c8-9e70d26ba598
keywords:
- 组父级 WDK 打印
- 常用属性页用户界面 WDK 打印，组父项
- CPSUI WDK 打印，组父项
- 属性表页 WDK 打印，组父项
- 对属性表页进行分组
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e34d3494cb46325580c4ee4d1a24c45efe4950ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526847"
---
# <a name="group-parent"></a>父级组





可以通过将它们分配给单个一起分组属性表页*父级组*。 您可以通过调用 CPSUI 的创建组父[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)函数与[ **CPSFUNC\_插入\_PSUIPAGE**](https://msdn.microsoft.com/library/windows/hardware/ff546414)函数的代码中，并指定 PSUIPAGEINSERT\_组\_作为父**类型**成员[ **INSERTPSUIPAGE\_信息** ](https://msdn.microsoft.com/library/windows/hardware/ff551634)结构。

创建新的组父级，则返回一个句柄。 然后可以为使用句柄*hComPropSheet*参数[ **ComPropSheet**](https://msdn.microsoft.com/library/windows/hardware/ff546207)，当添加或删除属性表页。

此外，作为接收组父句柄**hComPropSheet**的成员[ **PROPSHEETUI\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff561767)接收到的结构应用程序的[ **PFNPROPSHEETUI**](https://msdn.microsoft.com/library/windows/hardware/ff559812)-类型化的回调函数。 如果不创建新组的父项，则所有属性表页应都分配到此。

您可以创建其他组下创建每个组父级的父级。 属性表自身视为成为顶级组的父级。 如果未显式创建其他组的父级，所有添加的属性表页被分配到的顶级父级。

 

 




