---
title: 从驱动程序树中删除项
description: 从驱动程序树中删除项
ms.assetid: eea7565c-be15-4610-a1b4-16596d1daca2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 174d59206f65ce200393ea0e75fc457c9aa12b27
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840858"
---
# <a name="deleting-an-item-from-the-driver-tree"></a>从驱动程序树中删除项





为了删除驱动程序项，WIA 服务将调用微型驱动程序入口点[**IWiaMiniDrv：:D rvdeleteitem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvdeleteitem)。 在此方法中，微型驱动程序尝试删除 WIA 服务上下文参数*pWiasContext*指向的项。 如果成功删除项，则该方法返回\_OK，并将设备错误值参数*plDevErrVal*设置为零。 如果出现设备错误，该方法将在*plDevErrVal*中返回 FAILED 和设备特定的错误值。 微型驱动程序应调用[**wiasQueueEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiasqueueevent)函数来通知所有已连接的应用程序，该项已被删除。

删除根项后，WIA 服务将调用[**IWiaMiniDrv：:D rvfreedrvitemcontext**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvfreedrvitemcontext)以释放驱动程序特定的上下文使用的资源。 WIA 服务随后会删除该项和特定于驱动程序的上下文。

 

 




