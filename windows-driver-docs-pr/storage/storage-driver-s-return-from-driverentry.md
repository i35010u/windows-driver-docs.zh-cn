---
title: 存储驱动程序从 DriverEntry 返回的内容
description: 存储驱动程序从 DriverEntry 返回的内容
ms.assetid: a5772e9c-ec7b-4570-aaae-d2879f7e0bc7
keywords:
- 返回值 WDK SCSI
- ScsiPortInitialize
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e9d41262f3b4981bf18f5e808db818dbda53054
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63348457"
---
# <a name="storage-drivers-return-from-driverentry"></a>存储驱动程序从 DriverEntry 返回的内容


## <span id="ddk_storage_driver_s_return_from_driverentry_kg"></span><span id="DDK_STORAGE_DRIVER_S_RETURN_FROM_DRIVERENTRY_KG"></span>


当[ **ScsiPortInitialize** ](https://msdn.microsoft.com/library/windows/hardware/ff564645)控件，将返回[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)例程将返回的值传播到**ScsiPortInitialize**时**DriverEntry**本身返回控件。

如果微型端口驱动程序调用**ScsiPortInitialize**不止一次，其**DriverEntry**例程*必须传播 thelowest 值*返回的**ScsiPortInitialize**。 微型端口驱动程序编写器不能进行任何假设返回的值**ScsiPortInitialize**。

 

 




