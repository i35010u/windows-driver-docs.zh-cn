---
title: 在即插即用下进行的 SCSI 微型端口初始化
description: 在即插即用下进行的 SCSI 微型端口初始化
ms.assetid: bf2f9809-8271-4f0f-a2c4-25127fe9c4aa
keywords:
- SCSI 微型端口驱动程序 WDK 存储，PnP
- PnP WDK SCSI
- 即插即用 WDK SCSI
- 初始化 SCSI 微型端口驱动程序
- SCSI 微型端口驱动程序 WDK 存储，初始化
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5d060f37a54ab9b6f648823426de5b0205401229
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187779"
---
# <a name="scsi-miniport-initialization-under-plug-and-play"></a>在即插即用下进行的 SCSI 微型端口初始化

对于 Windows 2000 和更高版本，旧的微型端口驱动程序的初始化方式与 Microsoft Windows NT 4.0 完全相同。 当旧式微型端口驱动程序调用 [**ScsiPortInitialize**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportinitialize)时，端口驱动程序会调用微型端口驱动程序来查找并初始化其 HBA。 为每个 HBA 完成此操作，它找到的 (如果 HBA 位于可枚举总线上) 或重复，直到微型端口驱动程序报告它无法找到其他设备。 然后，控件返回到微型端口驱动程序的 [**DriverEntry**](driverentry-of-scsi-miniport-driver.md) 例程，其中微型端口驱动程序可以对不同类型的 HBA 再次调用 **ScsiPortInitialize** (例如，不同的接口或不同的供应商和产品 ID) 。 所有初始化调用都在微型端口驱动程序的 **DriverEntry** 例程的上下文中进行，并按调用 **ScsiPortInitialize** 的顺序进行。 旧驱动程序的初始化在系统启动时和在其他时间进行。

在即插即用中，无法保留初始化顺序。 当启用的即插即用微型端口驱动程序调用 **ScsiPortInitialize**时，端口驱动程序将存储初始化数据以供将来参考，然后返回 STATUS_SUCCESS。 此操作针对微型端口驱动程序的 **PnPInterface** 注册表项中列出的每个接口类型执行--该密钥中 *未* 列出的任何接口仍会立即初始化。

稍后，当即插即用 manager 检测到用于微型端口驱动程序的 HBA 时，它会通知端口驱动程序。 端口驱动程序为微型端口驱动程序的设备扩展分配所需的系统资源 (如内存) 并调用微型端口驱动程序查找 HBA，然后对其进行初始化。 在系统启动期间通常会发生这种情况，但当系统检测到插接操作或某个 HBA （如 CardBus）被热插拔到系统时也可能会发生这种情况。

即插即用管理器报告设备时，它已分配了总线资源 (例如，) 该设备 *和该*设备的 i/o 端口、内存地址和中断。 将这些资源提供给微型端口驱动程序，该驱动程序必须使用这些资源或报告找不到设备。 特别是，微型端口驱动程序不得尝试访问指定用于查找设备的端口或内存位置。

可能要求已作为即插即用驱动程序启动的微型端口驱动程序检测 nonenumerable 总线上的设备。 这包括总线，如 ISA，这要求总线上的微型端口驱动程序发出命令来查找 HBA。 此类检测中的设备会记录在注册表中，并在下次启动系统时作为即插即用设备进行初始化。

有关即插即用的详细信息，请参阅 [即插即用](https://docs.microsoft.com/windows-hardware/drivers/kernel/implementing-plug-and-play)。