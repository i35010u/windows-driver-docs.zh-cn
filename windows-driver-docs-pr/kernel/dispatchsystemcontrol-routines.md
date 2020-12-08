---
title: DispatchSystemControl 例程
description: DispatchSystemControl 例程
keywords:
- 调度例程 WDK 内核，DispatchSystemControl 例程
- 系统控制调度例程 WDK 内核
- IRP_MJ_SYSTEM_CONTROL i/o 函数代码
- DispatchSystemControl 例程
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa884664f4e4c816c99ccb3cfd83e0534752eff4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833435"
---
# <a name="dispatchsystemcontrol-routines"></a>DispatchSystemControl 例程





驱动程序的 [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 系统 \_ 控制**](./irp-mj-system-control.md) i/o 函数代码处理 irp。

所有驱动程序都必须提供 *DispatchSystemControl* 例程。 此例程的目的是为 Windows Management Instrumentation (WMI) 提供支持。 无论驱动程序是否支持 WMI，此例程都必须将 IRP 传递到下一个较低版本的驱动程序。

若要了解如何实现 *DispatchSystemControl* 例程以及如何在一般情况下支持 WMI，请参阅 [Windows Management Instrumentation](implementing-wmi.md)。

 

