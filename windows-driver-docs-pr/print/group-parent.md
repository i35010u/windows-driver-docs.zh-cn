---
title: 组的父级
description: 组的父级
keywords:
- 组父 WDK 打印
- 通用属性表用户界面 WDK 打印，组父项
- CPSUI WDK 打印，组父项
- 属性表页 WDK 打印，组父项
- 分组属性表页
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc6a886986217bd773fe69b92ac84b40477d411a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835853"
---
# <a name="group-parent"></a>组的父级





可以通过将属性表页分配给单个 *组父* 对象将它们组合在一起。 可以通过使用 [**CPSFUNC \_ INSERT \_ PSUIPAGE**](/previous-versions/ff546414(v=vs.85))函数代码调用 CPSUI 的 [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)函数来创建组父级，并指定 PSUIPAGEINSERT \_ 组 \_ parent 作为 [**INSERTPSUIPAGE \_ 信息**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_insertpsuipage_info)结构的 **类型** 成员。

当创建新的组父级时，将返回一个句柄。 然后，在添加或删除属性页时，该句柄可用作 [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet)的 *hComPropSheet* 参数。

此外，还会收到组父句柄，作为应用程序的 [**PFNPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)类型的回调函数接收到的 [**PROPSHEETUI \_ 信息**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_propsheetui_info)结构的 **hComPropSheet** 成员。 如果不创建新的组父项，则应将所有属性表页分配给此组。

你可以在创建的每个组父项下创建其他组父级。 属性表本身被视为顶级组父项。 如果未显式创建其他组父项，则会将所有添加的属性表页分配给顶级父级。

 

