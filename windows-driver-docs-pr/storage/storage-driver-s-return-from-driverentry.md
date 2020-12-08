---
title: 存储驱动程序从 DriverEntry 返回的内容
description: 存储驱动程序从 DriverEntry 返回的内容
keywords:
- 返回值 WDK SCSI
- ScsiPortInitialize
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: a339ad4869fe2e551e53cffa020f9d5d2eb38bd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799317"
---
# <a name="storage-drivers-return-from-driverentry"></a>存储驱动程序从 DriverEntry 返回的内容

当 [**ScsiPortInitialize**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)返回 control 时，当 **DriverEntry** 本身返回 control 时， [**DriverEntry**](driverentry-of-scsi-miniport-driver.md)例程将传播 **ScsiPortInitialize** 的返回值。

如果微型端口驱动程序多次调用 **ScsiPortInitialize** ，则其 **DriverEntry** 例程 *必须传播* **ScsiPortInitialize** 返回的 thelowest 值。 微型端口驱动程序编写器无法对 **ScsiPortInitialize** 返回的值作出任何假设。
