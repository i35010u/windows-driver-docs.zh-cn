---
title: 用于 Windows Vista 和 Windows XP 的单一驱动程序
description: 用于 Windows Vista 和 Windows XP 的单一驱动程序
ms.assetid: 3fa9c044-ab9d-4bed-b5fc-89396e1269ce
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1201153d40e55b3c0f520659a7d86aea8ba65e73
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840749"
---
# <a name="single-driver-for-windows-vista-and-windows-xp"></a>用于 Windows Vista 和 Windows XP 的单一驱动程序


你可能希望为 Windows Vista 和 Windows XP 使用单个驱动程序。 在这种情况下，驱动程序通过检查标志来处理数据传输。 当[**IWiaMiniDrv：** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)对基于流的传输调用:d rvacquireitemdata 时， *lFlags*参数将设置为 WIA\_MINIDRV\_传输\_下载或 WIA\_MINIDRV\_transfer\_上传。 如果这两个位均未设置，则表示传输为*传统*传输，驱动程序应遵循 Windows XP 数据传输中所述的行为。

 

 




