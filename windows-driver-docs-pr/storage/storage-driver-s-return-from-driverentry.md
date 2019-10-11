---
title: 存储驱动程序从 DriverEntry 返回的内容
description: 存储驱动程序从 DriverEntry 返回的内容
ms.assetid: a5772e9c-ec7b-4570-aaae-d2879f7e0bc7
keywords:
- 返回值 WDK SCSI
- ScsiPortInitialize
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 9a4eeacbf33c1793761fc00299bd4d2aaec3947f
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252402"
---
# <a name="storage-drivers-return-from-driverentry"></a>存储驱动程序从 DriverEntry 返回的内容

当[**ScsiPortInitialize**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/nf-srb-scsiportinitialize)返回 control 时，当**DriverEntry**本身返回 control 时， [**DriverEntry**](driverentry-of-scsi-miniport-driver.md)例程将传播**ScsiPortInitialize**的返回值。

如果微型端口驱动程序多次调用**ScsiPortInitialize** ，则其**DriverEntry**例程*必须传播* **ScsiPortInitialize**返回的 thelowest 值。 微型端口驱动程序编写器无法对**ScsiPortInitialize**返回的值作出任何假设。
