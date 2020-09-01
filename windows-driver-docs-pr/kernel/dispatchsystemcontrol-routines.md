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
ms.openlocfilehash: 6b1eb54ed9299f6859f47fcf05e37633ec2d8ca3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189789"
---
# <a name="dispatchsystemcontrol-routines"></a>DispatchSystemControl 例程





驱动程序的 [*DispatchSystemControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 系统 \_ 控制**](./irp-mj-system-control.md) i/o 函数代码处理 irp。

所有驱动程序都必须提供 *DispatchSystemControl* 例程。 此例程的目的是为 Windows Management Instrumentation (WMI) 提供支持。 无论驱动程序是否支持 WMI，此例程都必须将 IRP 传递到下一个较低版本的驱动程序。

若要了解如何实现 *DispatchSystemControl* 例程以及如何在一般情况下支持 WMI，请参阅 [Windows Management Instrumentation](implementing-wmi.md)。

 

