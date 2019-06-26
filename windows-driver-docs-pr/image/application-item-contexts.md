---
title: 应用程序项上下文
description: 应用程序项上下文
ms.assetid: d11b1750-999f-411c-9e83-6d2b20ce65db
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b978c24f9a58fb070bd494a8df861db60070f7a6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366757"
---
# <a name="application-item-contexts"></a>应用程序项上下文





应用程序项目的上下文，也称为*WIA 服务上下文*，是对 WIA 服务将传递给微型驱动程序中调用某一多个根或子项目的引用[IWiaMiniDrv 接口](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)方法。 当调用某些 WIA 服务库函数时，微型驱动程序然后使用此引用。 应用程序项上下文项指示哪一项是要处理的方法中。 微型驱动程序不应尝试直接访问应用程序项上下文。 微型驱动程序可以确定项通过调用驱动程序服务库函数，是根项还是子项目[ **wiasGetItemType**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasgetitemtype)。

当应用程序请求数据传输从设备到 WIA 项创建它时，它调用 WIA 服务以开始传输。 WIA 服务应用程序项目的上下文传递到微型驱动程序入口点等[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)方法。 随后，当微型驱动程序使用 WIA 服务库函数，如[ **wiasReadPropLong**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasreadproplong)，并通过应用程序项目上下文中的，WIA 服务读取从指定的属性与该应用程序项目关联的属性存储。

 

 




