---
title: ATA 端口的可以与存储类驱动程序交互的接口
description: ATA 端口的可以与存储类驱动程序交互的接口
ms.assetid: 6b22bbb1-f14e-48d9-a00c-c7eae79a078f
keywords:
- ATA 端口驱动程序 WDK，存储类驱动程序
- 存储类驱动程序 WDK，ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9304e2cecdecd69d1e55b95ed57704455ffb54b
ms.sourcegitcommit: e1ff1dd43b87dfb7349cebf70ed2878dc8d7c794
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2020
ms.locfileid: "75606491"
---
# <a name="ata-ports-interface-with-the-storage-class-driver"></a>ATA 端口的可以与存储类驱动程序交互的接口

> [!NOTE]
> ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用[storport 驱动](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-driver-overview)程序和[storport 微型端口](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-miniport-drivers)驱动程序模型。

ATA 端口驱动程序、SCSI 端口驱动程序和 Storport 驱动程序都使用 SRBs 来与较高级别的驱动程序（如存储类驱动程序）进行通信。 有关存储类和存储端口驱动程序之间的接口的详细信息，请参阅[具有存储类驱动程序的 SCSI 端口接口](scsi-port-s-srb-interface-with-the-storage-class-driver.md)。
