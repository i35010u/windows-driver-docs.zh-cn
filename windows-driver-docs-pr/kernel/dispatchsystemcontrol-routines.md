---
title: DispatchSystemControl 例程
description: DispatchSystemControl 例程
ms.assetid: b885a4a3-a9b6-423c-83bb-ee502724b0d0
keywords:
- 调度例程 WDK 内核，DispatchSystemControl 例程
- 系统控制调度例程 WDK 内核
- IRP_MJ_SYSTEM_CONTROL i/o 函数代码
- DispatchSystemControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14d4b1f204b9f6e30d0149993717b17388f12098
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836812"
---
# <a name="dispatchsystemcontrol-routines"></a>DispatchSystemControl 例程





驱动程序的[*DispatchSystemControl*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)例程为[**irp\_MJ\_SYSTEM\_控制**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mj-system-control)I/o 函数代码处理 irp。

所有驱动程序都必须提供*DispatchSystemControl*例程。 此例程旨在提供对 Windows Management Instrumentation （WMI）的支持。 无论驱动程序是否支持 WMI，此例程都必须将 IRP 传递到下一个较低版本的驱动程序。

若要了解如何实现*DispatchSystemControl*例程以及如何在一般情况下支持 WMI，请参阅[Windows Management Instrumentation](implementing-wmi.md)。

 

 




