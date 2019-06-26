---
title: Windows 内核模式 I/O 管理器
description: Windows 内核模式 I/O 管理器
ms.assetid: 8652f37d-0ece-4c08-9bce-499f0fedb0dd
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9e96566d4fd0d59f5fe539321c0b195d1947defe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358027"
---
# <a name="windows-kernel-mode-io-manager"></a>Windows 内核模式 I/O 管理器


计算机包含提供输入和输出 (I/O) 与外部世界的各种设备。 典型设备是键盘、 鼠标、 音频控制器、 视频控制器、 磁盘驱动器、 网络端口和等等。 设备驱动程序提供的设备和操作系统之间的软件连接。 出于此原因，I/O 是非常重要的设备驱动程序编写器。

Windows 内核模式 I/O 管理器管理应用程序和设备驱动程序提供的接口之间的通信。 设备运行速度可能会与操作系统不匹配，因为操作系统和设备驱动程序之间的通信主要是通过 I/O 请求数据包 (Irp)。 这些数据是类似于网络数据包或数据包 Windows 消息。 在传递到特定的驱动程序的操作系统从和到另一个驱动程序。

Windows I/O 系统提供分层驱动程序模型调用堆栈。 通常 Irp 转从一个驱动程序为另一种便于进行通信的同一堆栈。 例如，游戏杆驱动程序需要进行通信的 USB 集线器，又需要与 USB 主控制器，然后将需要通过计算机硬件的其余部分的 PCI 总线进行通信的通信。 堆栈组成游戏杆驱动程序、 USB 集线器、 USB 主控制器和 PCI 总线。 此通信协调将每个驱动程序放在堆栈发送和接收 Irp。

不能要着重强调足够您的驱动程序必须发送和接收 Irp 及时有效地操作整个堆栈。 如果您的驱动程序堆栈的一部分并不未正确接收、 处理和传递的信息，您的驱动程序可能会导致系统崩溃。

有关 Irp 的详细信息，请参阅[处理 Irp](handling-irps.md)。

有关驱动程序堆栈的详细信息，请参阅[设备对象和设备堆栈](device-objects-and-device-stacks.md)。

有关编程来与 I/O 管理相关，请参阅[I/O 管理器的编程技术](i-o-programming-techniques.md)。

为 I/O 管理器提供直接的界面的例程都通常带有前缀字母"**Io**"; 例如， **IoCreateDevice**。 I/O 管理器例程的列表，请参阅[I/O 管理器例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff551797(v=vs.85))。

有关与 IRP 相关的例程的列表，请参阅[Irp](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)。

I/O 管理器有两个子组件： 插管理器和电源管理器。 他们管理的插和电源管理的技术的 I/O 功能。 有关插管理的详细信息，请参阅[Windows 内核模式插管理器](windows-kernel-mode-plug-and-play-manager.md)和有关电源管理的详细信息，请参阅[Windows 内核模式电源管理器](windows-kernel-mode-power-manager.md)。

 

 




