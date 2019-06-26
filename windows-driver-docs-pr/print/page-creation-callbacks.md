---
title: 页面创建回调
description: 页面创建回调
ms.assetid: ec514d17-415e-417b-bb29-b37be43c3cf6
keywords:
- 回调函数 WDK CPSUI
- 常用属性页用户界面 WDK 打印，回调
- CPSUI WDK 打印，回调
- 属性表页 WDK 打印回调
- 页面创建回调 WDK CPSUI
- CommonPropertySheetUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7f0acb8e4d854044fc975e44653e8e9dabd3be4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360725"
---
# <a name="page-creation-callbacks"></a>页面创建回调





当应用程序进行初始调用到 CPSUI 的入口点函数 ([**CommonPropertySheetUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nf-compstui-commonpropertysheetuia))，它必须包含的地址[ **PFNPROPSHEETUI**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfnpropsheetui)-类型化的回调函数。 此回调函数负责描述属性表页和用于创建将这些说明发送到 CPSUI。

CPSUI 的**CommonPropertySheetUI**函数立即回调到 PFNPROPSHEETUI 类型化的函数提供的地址[ **PROPSHEETUI\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/ns-compstui-_propsheetui_info)结构。 然后，应用程序可以调用 CPSUI 的[ **ComPropSheet** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/compstui/nc-compstui-pfncompropsheet)函数，提供页描述 CPSUI 可用于创建页面，如以下关系图中所示：

![说明应用程序 cpsui 通信关系图](images/comprop.png)

有关详细信息，请参阅[方法指定页](methods-for-specifying-pages.md)。

 

 




