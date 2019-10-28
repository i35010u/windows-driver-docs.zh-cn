---
title: Windows 内核模式 WMI 库
description: Windows 内核模式 WMI 库
ms.assetid: ca981f38-8f3b-48cc-969f-ce53b85bba20
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 15c18e44e863edae920f1aad230e3a6dfd657732
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838306"
---
# <a name="windows-kernel-mode-wmi-library"></a>Windows 内核模式 WMI 库


Windows 提供了用于管理组件的常规机制。 此系统称为 Windows Management Instrumentation （WMI）。 若要 satisify Windows 驱动模型（WDM）要求，你应该为驱动程序实现 WMI，使你的驱动程序可由系统进行管理。

有关 WMI 的详细信息，请参阅[Windows Management Instrumentation](implementing-wmi.md)。

为 WMI 库提供直接接口的例程的前缀为 "**wmi**";有关 WMI 例程的列表，请参阅[Windows Management Instrumentation （WMI）库例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

有关 WMI 回调的列表，请参阅[Wmi 库回调例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

与 WMI 的通信是通过 Irp 来完成的。 有关驱动程序可用于接收 Irp 的例程列表，请参阅[WMI IRP 处理例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 有关驱动程序可用于发送 WMI Irp 的例程列表，请参阅[WMI IRP 发送例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。 有关与 WMI 一起使用的 Irp 列表，请参阅[Wmi 次要 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/wmi-minor-irps)。

 

 




