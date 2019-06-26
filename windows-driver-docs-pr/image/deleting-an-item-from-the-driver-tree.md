---
title: 从驱动程序树中删除项
description: 从驱动程序树中删除项
ms.assetid: eea7565c-be15-4610-a1b4-16596d1daca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c9a90ca163f6f729995bad4d035d9094234fc88
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67353804"
---
# <a name="deleting-an-item-from-the-driver-tree"></a>从驱动程序树中删除项





若要删除的驱动程序项，WIA 服务调用微型驱动程序入口点[ **IWiaMiniDrv::drvDeleteItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)。 在此方法，微型驱动程序将尝试删除 WIA 服务上下文参数的项*pWiasContext*点。 如果成功删除该项，则该方法返回 S\_确定，并设置设备错误值参数， *plDevErrVal*、 为零。 如果设备出错，则方法返回失败和中的特定于设备的错误值*plDevErrVal*。 微型驱动程序应调用[ **wiasQueueEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamdef/nf-wiamdef-wiasqueueevent)函数来通知所有连接的应用程序已删除了某项。

WIA 服务根项已被删除后，调用[ **IWiaMiniDrv::drvFreeDrvItemContext** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)来释放使用的驱动程序特定的上下文的资源。 WIA 服务然后会删除项和特定于驱动程序的上下文。

 

 




