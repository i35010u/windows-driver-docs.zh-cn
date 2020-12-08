---
title: ATA 端口 i/o 模型概述
description: ATA 端口 i/o 模型概述
keywords:
- ATA 端口驱动程序 WDK，i/o
- I/o WDK ATA 端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c678711e886260e0daf6f0b9f9b0970663fbd357
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811787"
---
# <a name="ata-port-io-model-overview"></a>ATA 端口 i/o 模型概述

> [!NOTE]
> ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](./storport-driver-overview.md) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。

与 Storport 驱动程序一样，ATA 端口驱动程序使用 i/o 的推送模式。 这意味着，驱动程序会将 i/o 请求异步转发到其微型端口驱动程序，直到达到最大数量的重叠数据包，而无需等待微型端口驱动程序请求输入。 在推送模型中，端口驱动程序控制 i/o 请求的流动，并将请求推送到微型端口驱动程序。

另一方面，SCSI 端口驱动程序使用 i/o 的请求模型。 在 i/o 的请求模型中，SCSI 端口驱动程序会以同步方式将 i/o 请求转发到其微型端口驱动程序，并等待微型端口驱动程序在发送下一个 i/o 请求之前请求新输入。 此外，微型端口驱动程序控制 i/o 请求的流，并从端口驱动程序中取出请求。

有关 Storport 驱动程序的 i/o 模型的详细信息，请参阅 [storport I/o 型号](storport-i-o-model.md)。

有关 SCSI 端口驱动程序的 i/o 模型的详细信息，请参阅 [Scsi 端口 I/o 型号](scsi-port-i-o-model.md)。
