---
title: SCSI 微型端口驱动程序的 HwScsiAdapterState 例程
description: SCSI 微型端口驱动程序的 HwScsiAdapterState 例程
ms.assetid: 359c41ba-b8d9-4e2d-87d7-025db377606b
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiAdapterState
- HwScsiAdapterState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24144f42be36e851d16fb1d348e1cf8ad137c754
ms.sourcegitcommit: 5f4252ee4d5a72fa15cf8c68a51982c2bc6c8193
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252458"
---
# <a name="scsi-miniport-drivers-hwscsiadapterstate-routine"></a>SCSI 微型端口驱动程序的 HwScsiAdapterState 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiadapterstate_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERSTATE_ROUTINE_KG"></span>


在基于 NT 的操作系统中，[小型端口驱动](scsi-miniport-driver-routines.md)程序应仅在以下条件之一保留时，才在[**HW @ no__t-3INITIALIZATION @ no__t-4DATA （scsi）** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/srb/ns-srb-_hw_initialization_data)中将此入口点设置为**NULL** ：

-   微型端口驱动程序驱动一个 HBA，使其连接到通常只在基于 RISC 的高端平台中找到的 i/o 总线上。 也就是说，运行仅支持 x86 的 Microsoft Windows 系统的基于 x86 的平台将不具有类型的 i/o 总线来支持 HBA。

-   微型端口驱动程序驱动了可在运行仅限 x86 的 Windows 系统的基于 x86 的平台中找到的 HBA，但 HBA 既没有 BIOS 也没有纯模式的实模式驱动程序。

否则，微型端口驱动程序必须具有可在基于 NT 的操作系统和仅限 x86 的 Microsoft Windows 系统之间移植的*HwScsiAdapterState*例程。

[**HwScsiAdapterState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85))例程负责保存和还原其 HBA 的状态，这是由仅限 x86 的系统在 x86 real 和 protected processor 模式间转换时所要求的。

有关详细信息，请参阅[**HwScsiAdapterState**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557278(v=vs.85)) 。

 

 




