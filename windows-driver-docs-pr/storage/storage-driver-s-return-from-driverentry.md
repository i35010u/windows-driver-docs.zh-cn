---
title: 存储驱动程序从 DriverEntry 返回的内容
description: 存储驱动程序从 DriverEntry 返回的内容
ms.assetid: a5772e9c-ec7b-4570-aaae-d2879f7e0bc7
keywords:
- 返回值 WDK SCSI
- ScsiPortInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaf808b5a83f89af3eb050b63d09bacbd635dc96
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368855"
---
# <a name="storage-drivers-return-from-driverentry"></a>存储驱动程序从 DriverEntry 返回的内容


## <span id="ddk_storage_driver_s_return_from_driverentry_kg"></span><span id="DDK_STORAGE_DRIVER_S_RETURN_FROM_DRIVERENTRY_KG"></span>


当[ **ScsiPortInitialize** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)控件，将返回[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)例程将返回的值传播到**ScsiPortInitialize**时**DriverEntry**本身返回控件。

如果微型端口驱动程序调用**ScsiPortInitialize**不止一次，其**DriverEntry**例程*必须传播 thelowest 值*返回的**ScsiPortInitialize**。 微型端口驱动程序编写器不能进行任何假设返回的值**ScsiPortInitialize**。

 

 




