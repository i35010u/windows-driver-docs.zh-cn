---
title: Windows 内核模式 WMI 库
description: Windows 内核模式 WMI 库
ms.assetid: ca981f38-8f3b-48cc-969f-ce53b85bba20
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 75c2219afc56dec639e6fa0b5a24de535dc7ee54
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89193069"
---
# <a name="windows-kernel-mode-wmi-library"></a>Windows 内核模式 WMI 库


Windows 提供了用于管理组件的常规机制。  (WMI) Windows Management Instrumentation 调用此系统。 若要 satisify Windows 驱动模型 (WDM) 要求，你应该为驱动程序实现 WMI，使你的驱动程序可以由系统进行管理。

有关 WMI 的详细信息，请参阅 [Windows Management Instrumentation](implementing-wmi.md)。

为 WMI 库提供直接接口的例程的前缀为 "**wmi**";有关 WMI 例程的列表，请参阅 [Windows Management Instrumentation (wmi) 库例程](/windows-hardware/drivers/ddi/index)。

有关 WMI 回调的列表，请参阅 [Wmi 库回调例程](/windows-hardware/drivers/ddi/index)。

与 WMI 的通信是通过 Irp 来完成的。 有关驱动程序可用于接收 Irp 的例程列表，请参阅 [WMI IRP 处理例程](/windows-hardware/drivers/ddi/index)。 有关驱动程序可用于发送 WMI Irp 的例程列表，请参阅 [WMI IRP 发送例程](/windows-hardware/drivers/ddi/index)。 有关与 WMI 一起使用的 Irp 列表，请参阅 [Wmi 次要 irp](./wmi-minor-irps.md)。

 

