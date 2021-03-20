---
title: 与存储端口驱动程序通信
description: 存储微型端口如何与存储端口驱动程序通信
keywords:
- 存储微型端口驱动程序 WDK
- 微型端口驱动程序 WDK 存储
- 存储驱动程序 WDK，微型端口驱动程序
- 存储微型端口应避免调用操作系统例程
ms.date: 03/16/2021
ms.localizationpriority: medium
ms.openlocfilehash: 301eebad25603fd0047e0a2e0d738fb4e541d381
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719987"
---
# <a name="communicating-with-a-storage-port-driver"></a>与存储端口驱动程序通信

存储微型端口驱动程序和系统提供的存储端口驱动程序之间的通信如下所示：

- 小型端口调用一组存储端口驱动程序提供的支持例程

- 小型端口实现了一组标准例程，用于调用它的存储端口驱动程序，一些是必需的，一些是可选的

SCSI 端口驱动程序、Storport 驱动程序和 ATA 端口驱动程序调用的微型端口驱动程序例程非常类似。

存储微型端口驱动程序应避免调用操作系统 (操作系统) 例程，而不是由适当的端口驱动程序支持提供的支持例程。 例如：

- 存储微型端口驱动程序不应调用 [**KeQuerySystemTime**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kequerysystemtime)，而应调用 [**ScsiPortQuerySystemTime**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportquerysystemtime) 或 [**StorPortQuerySystemTime**](/windows-hardware/drivers/ddi/storport/nf-storport-storportquerysystemtime)等例程。
- 存储微型端口驱动程序不应调用 [**MmGetPhysicalAddress**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmgetphysicaladdress)，而应调用 [**ScsiPortGetPhysicalAddress**](/windows-hardware/drivers/ddi/srb/nf-srb-scsiportgetphysicaladdress) 和 [**StorPortGetPhysicalAddress**](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetphysicaladdress)之类的例程。

> [!NOTE]
> 如果需要对 windows[硬件兼容程序](/windows-hardware/design/compatibility/)进行调用，则需要将[存储导入测试](/windows-hardware/test/hlk/testref/c75585b2-a3e6-4db0-8847-f6023171d4b9)视为 windows 预设备的小型小型驱动程序将会失败。

不要在微型端口驱动程序中使用 [硬件抽象层例程](/previous-versions/windows/hardware/drivers/ff546644(v=vs.85)) 。
