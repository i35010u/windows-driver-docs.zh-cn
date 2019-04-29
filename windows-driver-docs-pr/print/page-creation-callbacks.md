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
ms.openlocfilehash: a8ac765e8dfc4963f45d7fcc434ea102ede65b08
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353719"
---
# <a name="page-creation-callbacks"></a>页面创建回调





当应用程序进行初始调用到 CPSUI 的入口点函数 ([**CommonPropertySheetUI**](https://msdn.microsoft.com/library/windows/hardware/ff546148))，它必须包含的地址[ **PFNPROPSHEETUI**](https://msdn.microsoft.com/library/windows/hardware/ff559812)-类型化的回调函数。 此回调函数负责描述属性表页和用于创建将这些说明发送到 CPSUI。

CPSUI 的**CommonPropertySheetUI**函数立即回调到 PFNPROPSHEETUI 类型化的函数提供的地址[ **PROPSHEETUI\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff561767)结构。 然后，应用程序可以调用 CPSUI 的[ **ComPropSheet** ](https://msdn.microsoft.com/library/windows/hardware/ff546207)函数，提供页描述 CPSUI 可用于创建页面，如以下关系图中所示：

![说明应用程序 cpsui 通信关系图](images/comprop.png)

有关详细信息，请参阅[方法指定页](methods-for-specifying-pages.md)。

 

 




