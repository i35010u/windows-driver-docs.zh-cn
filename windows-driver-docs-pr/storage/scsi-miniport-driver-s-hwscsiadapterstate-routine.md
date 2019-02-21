---
title: SCSI 微型端口驱动程序的 HwScsiAdapterState 例程
description: SCSI 微型端口驱动程序的 HwScsiAdapterState 例程
ms.assetid: 359c41ba-b8d9-4e2d-87d7-025db377606b
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiAdapterState
- HwScsiAdapterState
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c03eba403e11736f72df927c640b71d3a448cf6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524266"
---
# <a name="scsi-miniport-drivers-hwscsiadapterstate-routine"></a>SCSI 微型端口驱动程序的 HwScsiAdapterState 例程


## <span id="ddk_scsi_miniport_drivers_hwscsiadapterstate_routine_kg"></span><span id="DDK_SCSI_MINIPORT_DRIVERS_HWSCSIADAPTERSTATE_ROUTINE_KG"></span>


在基于 NT 的操作系统，微型端口驱动程序应将此入口点设置为**NULL**中[ **HW\_初始化\_数据 (SCSI)** ](https://msdn.microsoft.com/library/windows/hardware/ff557456) (请参阅[必需和可选 SCSI 微型端口驱动程序例程](required-and-optional-scsi-miniport-driver-routines.md)) 仅当以下条件之一保存：

-   微型端口驱动程序驱动器连接仅在高端的 risc 平台中常见的 I/O 总线上的 HBA。 也就是说，运行的仅限 x86 的 Microsoft Windows 系统的基于 x86 的平台不会以支持 HBA 的类型的 I/O 总线。

-   微型端口驱动程序驱动器在运行仅限 x86 的 Windows 系统中，基于 x86 的平台中找到的 HBA 但 HBA 具有 BIOS 和仅限 x86 的实模式驱动程序都不。

否则，微型端口驱动程序必须具有*HwScsiAdapterState*例程，可在基于 NT 的操作系统和仅限 x86 的 Microsoft Windows 系统之间移植性。

一个[ **HwScsiAdapterState** ](https://msdn.microsoft.com/library/windows/hardware/ff557278)例程负责保存和还原其 HBA 的状态在 x86 之间的转换过程的仅限 x86 的系统要求，其实部和受保护的处理器模式。

请参阅[ **HwScsiAdapterState** ](https://msdn.microsoft.com/library/windows/hardware/ff557278)有关详细信息。

 

 




