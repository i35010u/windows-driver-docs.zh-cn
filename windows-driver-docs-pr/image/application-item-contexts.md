---
title: 应用程序项上下文
description: 应用程序项上下文
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62e31a334da765e475be03ae1ccc4f04749eccb7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828747"
---
# <a name="application-item-contexts"></a>应用程序项上下文





应用程序项上下文（也称为 *WIA 服务上下文*）是对一个根项或子项的引用，WIA 服务在对几个 [IWiaMiniDrv 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv) 方法之一的调用中传递给微型驱动程序。 然后，微型驱动程序在调用某些 WIA 服务库函数时使用此引用。 项目的应用程序项上下文指示要在方法中处理的项。 微型驱动程序不应尝试直接访问应用程序项上下文。 微型驱动程序可以通过调用驱动程序服务库函数 [**wiasGetItemType**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasgetitemtype)来确定项是根项还是子项项。

当应用程序请求将数据从设备传输到它创建的 WIA 项时，它会调用 WIA 服务来启动传输。 WIA 服务将应用程序项的上下文传递给微型驱动程序入口点，如 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata) 方法。 接下来，当微型驱动程序使用 WIA 服务库函数（如 [**wiasReadPropLong**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasreadproplong)）并在应用程序项上下文中传递时，WIA 服务从与该应用程序项关联的属性存储读取指定的属性。

 

