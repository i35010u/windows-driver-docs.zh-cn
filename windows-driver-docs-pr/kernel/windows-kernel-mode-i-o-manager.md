---
title: Windows 内核模式 I/O 管理器
description: Windows 内核模式 I/O 管理器
ms.assetid: 8652f37d-0ece-4c08-9bce-499f0fedb0dd
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7d4ec34a962dc884363250fbaff2db2347e9a47f
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190257"
---
# <a name="windows-kernel-mode-io-manager"></a>Windows 内核模式 I/O 管理器


计算机由各种设备组成，它们提供与外部世界之间 (i/o) 的输入和输出。 典型设备包括键盘、鼠标、音频控制器、视频控制器、磁盘驱动器、网络端口等。 设备驱动程序在设备和操作系统之间提供软件连接。 出于此原因，i/o 对设备驱动程序编写器非常重要。

Windows 内核模式 i/o 管理器管理应用程序与设备驱动程序提供的接口之间的通信。 由于设备的运行速度可能与操作系统不匹配，因此，操作系统和设备驱动程序之间的通信主要通过 i/o 请求数据包 (Irp) 完成。 这些数据包与网络数据包或 Windows 消息数据包类似。 它们从操作系统传递到特定驱动程序，并从一个驱动程序传递到另一个驱动程序。

Windows i/o 系统提供名为 stack 的分层驱动程序模型。 通常，在同一堆栈中，Irp 从一个驱动程序传输到另一个驱动程序，以便进行通信。 例如，游戏杆驱动程序需要与 USB 集线器通信，这反过来需要与 USB 主机控制器通信，然后需要通过 PCI 总线与计算机硬件的其余部分通信。 堆栈包含游戏杆驱动程序、USB 集线器、USB 主机控制器和 PCI 总线。 此通信通过使堆栈发送和接收 Irp 中的每个驱动程序进行协调。

它的意义不大，您的驱动程序必须及时发送和接收 Irp，整个堆栈才能有效地运行。 如果你的驱动程序是堆栈的一部分，并且没有正确接收、处理和传递这些信息，你的驱动程序可能会导致系统崩溃。

有关 Irp 的详细信息，请参阅 [处理 irp](handling-irps.md)。

有关驱动程序堆栈的详细信息，请参阅 [设备对象和设备堆栈](device-objects-and-device-stacks.md)。

有关与 i/o 管理相关的编程能够，请参阅 [I/o 管理器编程技术](i-o-programming-techniques.md)。

向 i/o 管理器提供直接接口的例程通常以字母 "**Io**" 作为前缀;例如， **IoCreateDevice**。 有关 i/o 管理器例程的列表，请参阅 [I/o 管理器例程](/previous-versions/windows/hardware/drivers/ff551797(v=vs.85))。

有关与 IRP 相关的例程列表，请参阅 [irp](/windows-hardware/drivers/ddi/index)。

I/o 管理器有两个子组件：即插即用 manager 和电源管理器。 它们针对即插即用和电源管理的技术管理 i/o 功能。 有关即插即用管理的详细信息，请参阅 [Windows 内核模式即插即用管理器](windows-kernel-mode-plug-and-play-manager.md) 和有关电源管理的详细信息，请参阅 [Windows 内核模式电源管理器](windows-kernel-mode-power-manager.md)。

 

