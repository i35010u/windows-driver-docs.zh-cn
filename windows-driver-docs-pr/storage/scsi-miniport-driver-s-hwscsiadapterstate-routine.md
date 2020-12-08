---
title: SCSI 微型端口驱动程序的 HwScsiAdapterState 例程
description: SCSI 微型端口驱动程序的 HwScsiAdapterState 例程
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiAdapterState
- HwScsiAdapterState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8e9ddecf832597009eba916e179db1c31d6aa8c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837097"
---
# <a name="scsi-miniport-drivers-hwscsiadapterstate-routine"></a>SCSI 微型端口驱动程序的 HwScsiAdapterState 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiadapterstate_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERSTATE_ROUTINE_KG"></span>


在基于 NT 的操作系统中，微型端口驱动程序应在 [**HW \_ 初始化 \_ 数据 (SCSI)**](/windows-hardware/drivers/ddi/srb/ns-srb-_hw_initialization_data)中将此入口点设置为 **NULL** (请参阅仅当满足以下任一条件时，才) [scsi 微型端口驱动程序例程](scsi-miniport-driver-routines.md)：

-   微型端口驱动程序驱动一个 HBA，使其连接到通常只在基于 RISC 的高端平台中找到的 i/o 总线上。 也就是说，运行仅支持 x86 的 Microsoft Windows 系统的基于 x86 的平台将不具有类型的 i/o 总线来支持 HBA。

-   微型端口驱动程序驱动了可在运行仅限 x86 的 Windows 系统的基于 x86 的平台中找到的 HBA，但 HBA 既没有 BIOS 也没有纯模式的实模式驱动程序。

否则，微型端口驱动程序必须具有可在基于 NT 的操作系统和仅限 x86 的 Microsoft Windows 系统之间移植的 *HwScsiAdapterState* 例程。

[**HwScsiAdapterState**](/previous-versions/windows/hardware/drivers/ff557278(v=vs.85))例程负责保存和还原其 HBA 的状态，这是由仅限 x86 的系统在 x86 real 和 protected processor 模式间转换时所要求的。

有关详细信息，请参阅 [**HwScsiAdapterState**](/previous-versions/windows/hardware/drivers/ff557278(v=vs.85)) 。

 

