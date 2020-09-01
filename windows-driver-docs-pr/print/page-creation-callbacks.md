---
title: 页面创建回调
description: 页面创建回调
ms.assetid: ec514d17-415e-417b-bb29-b37be43c3cf6
keywords:
- 回调函数 WDK CPSUI
- 公共属性表用户界面 WDK 打印，回调
- CPSUI WDK 打印，回调
- 属性表页 WDK 打印，回调
- 页面创建回调 WDK CPSUI
- CommonPropertySheetUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b482ee4347545df558235e0426d4c0cd408edb75
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89218199"
---
# <a name="page-creation-callbacks"></a>页面创建回调





当应用程序初始调用 CPSUI 的入口点函数 ([**CommonPropertySheetUI**](/windows-hardware/drivers/ddi/compstui/nf-compstui-commonpropertysheetuia)) 时，它必须包含 [**PFNPROPSHEETUI**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfnpropsheetui)类型的回调函数的地址。 此回调函数负责描述属性表页面，并将这些说明发送到 CPSUI 进行创建。

CPSUI 的 **CommonPropertySheetUI** 函数立即返回 PFNPROPSHEETUI 类型的函数，并提供 [**PROPSHEETUI \_ 信息**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_propsheetui_info) 结构的地址。 然后，应用程序可以调用 CPSUI 的 [**ComPropSheet**](/windows-hardware/drivers/ddi/compstui/nc-compstui-pfncompropsheet) 函数，同时提供 CPSUI 可用于创建页面的页面说明，如下图所示：

![说明应用程序 cpsui 通信的示意图](images/comprop.png)

有关详细信息，请参阅 [指定页的方法](methods-for-specifying-pages.md)。

 

