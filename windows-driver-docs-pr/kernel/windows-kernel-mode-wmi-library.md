---
title: Windows 内核模式 WMI 库
description: Windows 内核模式 WMI 库
ms.assetid: ca981f38-8f3b-48cc-969f-ce53b85bba20
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 84d834e8c8efed50820882e959de43ad5e77a662
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63393016"
---
# <a name="windows-kernel-mode-wmi-library"></a>Windows 内核模式 WMI 库


Windows 提供了用于管理组件的常规机制。 此系统称为 Windows Management Instrumentation (WMI)。 Satisify Windows 驱动程序模型 (WDM) 要求，应为您的驱动程序实现 WMI，以便可以由系统管理您的驱动程序。

有关 WMI 的详细信息，请参阅[Windows Management Instrumentation](implementing-wmi.md)。

为提供 WMI 库的直接接口的例程都带有前缀字母"**Wmi**"; 有关 WMI 例程的列表，请参阅[Windows Management Instrumentation (WMI) 库例程](https://msdn.microsoft.com/library/windows/hardware/ff566359)。

有关 WMI 的回调的列表，请参阅[WMI 库回调例程](https://msdn.microsoft.com/library/windows/hardware/ff566357)。

与 WMI 的通信是通过 Irp。 可以使用您的驱动程序接收 Irp 的例程的列表，请参阅[WMI IRP 处理例程](https://msdn.microsoft.com/library/windows/hardware/ff566353)。 可以使用您的驱动程序发送 WMI Irp 的例程的列表，请参阅[WMI IRP 发送例程](https://msdn.microsoft.com/library/windows/hardware/ff566355)。 结合 WMI 使用的 Irp 的列表，请参阅[WMI 次要 Irp](https://msdn.microsoft.com/library/windows/hardware/ff566361)。

 

 




