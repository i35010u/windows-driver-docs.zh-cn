---
title: ATA 端口驱动程序概述
description: ATA 端口驱动程序概述
keywords:
- 存储端口驱动程序 WDK，ATA 端口驱动程序
- ATA 端口驱动程序 WDK
- ATA 端口驱动程序 WDK，关于 ATA 端口驱动程序
- IDE 控制器 WDK ATA 端口驱动程序
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: c29bbf16902a0ec091d7fc69bf2e9e4824d13cc9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804775"
---
# <a name="ata-port-driver-overview"></a>ATA 端口驱动程序概述

> [!NOTE]
> ATA 端口驱动程序和 ATA 微型端口驱动程序模型可能会在将来更改或不可用。 相反，我们建议使用 [storport 驱动](storport-driver-overview.md) 程序和 [storport 微型端口](./storport-miniport-drivers.md) 驱动程序模型。

除了 [SCSI 端口驱动程序](scsi-port-driver-overview.md) 和 [Storport 驱动程序](storport-driver-overview.md)以外，windows Vista 和更高版本的 WINDOWS 操作系统还提供 ATA 端口驱动程序 (*Ataport.sys*) ，这是一个特别适用于 IDE 控制器的存储端口驱动程序。

ATA 端口驱动程序和其他系统提供的存储端口驱动程序之间的最大差别在于 ATA 端口驱动程序用来与其他驱动程序通信的协议。 所有其他系统提供的存储端口驱动程序都使用 (SRBs) 的 SCSI 请求块与更高级的驱动程序（如存储类驱动程序）和微型端口驱动程序通信。 ATA 端口驱动程序使用 SRBs 仅与更高级别驱动程序通信。 ATA 端口使用称为 IDE 请求块 () 的数据包，该数据包由 [IDE_REQUEST_BLOCK](/windows-hardware/drivers/ddi/irb/ns-irb-_ide_request_block) 结构定义。 IRBs 比 SRBs ATA 设备特征更好。

ATA 端口驱动程序和其他系统提供的存储驱动程序的另一个不同之处在于 ATA 端口驱动程序会禁止 ATA 微型端口驱动程序满足 SCSI 标准定义的某些要求。 例如，ATA 端口驱动程序使用 ATA 命令从 ATA 微型端口驱动程序收集等效的 SCSI 感知数据，转换数据，使其符合 SCSI 感知数据格式，并将数据传递给较高级别的驱动程序，就像它是 SCSI 感知数据一样。 因此，ATA 微型端口驱动程序无需直接响应来自更高级别的驱动程序的 SCSI 感知数据请求。

ATA 微型端口驱动程序接口非常类似于 SCSI 端口驱动程序接口。 因此，如果你已经编写了一个 SCSI 微型端口驱动程序，你应该能够轻松了解如何编写 ATA 微型端口驱动程序。 当前 ATA/ATAPI 技术的驱动程序（例如串行 ATA (SATA) ）应使用更高的性能 Storport 微型端口接口。

除了 ATA 端口驱动程序，操作系统还提供默认的 ATA 微型端口驱动程序和默认控制器微型驱动程序。 系统提供的默认驱动程序适用于大多数控制器硬件，我们强烈建议尽可能使用默认微型驱动程序。
