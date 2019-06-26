---
title: 用于 Windows Vista 和 Windows XP 的单一驱动程序
description: 用于 Windows Vista 和 Windows XP 的单一驱动程序
ms.assetid: 3fa9c044-ab9d-4bed-b5fc-89396e1269ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c8df16e228eed7b90bdc8d800addebf625aeaf5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386910"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>用于 Windows Vista 和 Windows XP 的单一驱动程序


您可能想要为 Windows Vista 和 Windows XP 单个驱动程序。 在这种情况下，该驱动程序通过检查标志来处理数据传输。 当[ **IWiaMiniDrv::drvAcquireItemData** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)称为基于流的传输*lFlags*参数设置为任一 WIA\_MINIDRV\_传输\_下载或 WIA\_MINIDRV\_传输\_上传。 如果这些位未设置，则传输*旧*传输和驱动程序应遵循的 Windows XP 数据传输所述的行为。

 

 




