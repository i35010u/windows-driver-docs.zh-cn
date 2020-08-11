---
title: 内核模式驱动程序体系结构设计指南
description: 内核模式驱动程序体系结构设计指南
ms.assetid: 21c199f3-abc3-4607-a674-eb84b6c3c25a
keywords:
- 内核模式驱动程序 WDK，体系结构
- 内核模式驱动程序 WDK
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: cf31a5dd983bd0154c7094e9cfdfdcf70df3f52f
ms.sourcegitcommit: 4801d5c3767daf77743dd0f4016116ecaf54cd55
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/06/2020
ms.locfileid: "87838451"
---
# <a name="kernel-mode-driver-architecture-design-guide"></a>内核模式驱动程序体系结构设计指南

>[!NOTE]
>有关你的驱动程序可以实现或调用的编程接口的详细信息，请参阅[内核模式驱动程序参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)。

本部分提供了一般概念来帮助你了解内核模式编程，并介绍了内核编程的特定技术。 有关 Windows 驱动程序的总体概述，请参阅 [Windows 驱动程序入门](../develop/getting-started-with-windows-drivers.md)，其中提供了 Windows 组件的总体概述，列出了 Windows 中使用的设备驱动程序的类型，讨论了 Windows 设备驱动程序的目标，并讨论了工具包中包括的泛型示例设备驱动程序。

本节包含的概念信息可在你构建内核模式驱动程序时提供指导和帮助。

- 包含以下内容的概述：
  - [Windows 组件概述](overview-of-windows-components.md)
  - [内核模式驱动程序的设计目标](design-goals-for-kernel-mode-drivers.md)
  - [示例内核模式驱动程序](sample-kernel-mode-drivers.md)的目录
  - 由 Microsoft Surface 团队编译的[核心驱动程序开发最佳做法](surface-team-driver-development-best-practices.md)

- “内核模式组件”描述了 Windows 操作系统的主要内核模式管理器和组件。

  |组件|描述|
  |----|----|
  |管理器||
  |[Windows 内核模式对象管理器](windows-kernel-mode-object-manager.md)|管理对象：文件、设备、同步机制、注册表项等。|
  |[Windows 内核模式内存管理器](windows-kernel-mode-memory-manager.md)|管理操作系统的物理内存。|
  |[Windows 内核模式进程和线程管理器](windows-kernel-mode-process-and-thread-manager.md)|处理进程中所有线程的执行。|
  |[Windows 内核模式 I/O 管理器](windows-kernel-mode-i-o-manager.md)|管理应用程序与设备驱动程序所提供的接口之间的通信。|
  |[Windows 内核模式即插即用管理器](windows-kernel-mode-plug-and-play-manager.md)|I/O 管理器的一个子系统 - 即插即用 (PnP) 管理器，使电脑能够识别设备添加到系统的时间。|
  |[Windows 内核模式电源管理器](windows-kernel-mode-power-manager.md)|为支持电源状态更改的所有设备管理电源状态的有序更改。|
  |[Windows 内核模式配置管理器](windows-kernel-mode-configuration-manager.md)|管理注册表，如监视注册表中的更改或针对特定注册表数据注册回调。|
  |[Windows 内核模式内核事务管理器](windows-kernel-mode-kernel-transaction-manager.md)|在内核模式下实现事务处理。|
  |[Windows 内核模式安全引用监视器](windows-kernel-mode-security-reference-monitor.md)|为驱动程序提供使用访问控制的例程。|
  |**库**||
  |[Windows 内核模式内核库](windows-kernel-mode-kernel-library.md)|实现操作系统中的所有其他内容所依赖的核心功能。 Microsoft Windows 内核提供基本的低级操作，如计划线程或路由硬件中断。|
  |[Windows 内核模式执行支持库](windows-kernel-mode-executive-support-library.md)|指的是向设备驱动程序提供各种服务的内核模式组件，这些服务包括：对象管理、内存管理、进程和线程管理、输入/输出管理和配置管理。|
  |[Windows 内核模式运行时库](windows-kernel-mode-run-time-library.md)|各种内核模式组件所需的一组常用实用工具例程。|
  |[Windows 内核模式安全字符串库](windows-kernel-mode-safe-string-library.md)|一个安全字符串库，用于在内核模式开发中提供更高的安全性。|
  |[Windows 内核模式 DMA 库](windows-kernel-mode-dma-library.md)|适用于设备驱动程序开发人员的直接内存访问 (DMA) 库。|
  |[Windows 内核模式 HAL 库](windows-kernel-mode-hal-library.md)|适用于内核模式驱动程序开发的硬件抽象层 (HAL)。|
  |[Windows 内核模式 CLFS 库](windows-kernel-mode-clfs-library.md)|事务日志记录系统，即公用日志文件系统 (CLFS)。|
  |[Windows 内核模式 WMI 库](windows-kernel-mode-wmi-library.md)|用于管理组件的常规机制，称为 Windows Management Instrumentation (WMI)。|

- [编写 WDM 驱动程序](writing-wdm-drivers.md)和 [WDM 简介](introduction-to-wdm.md)提供了使用 Windows 驱动模型 (WDM) 编写驱动程序时所需的信息。

- [设备对象](introduction-to-device-objects.md)和“设备对象和设备堆栈”中的其他主题介绍操作系统如何通过设备对象来表示设备 。

- [Windows 驱动程序的内存管理](managing-memory-for-drivers.md)说明了内核模式驱动程序如何分配内存，用于存储内部数据、在 I/O 操作期间缓冲数据以及与其他内核模式和用户模式组件共享内存等目的。

- [控制设备访问](controlling-device-access.md)的安全性和[设备对象 SDDL](sddl-for-device-objects.md)的[特权](privileges.md)可确保驱动程序尽可能安全。

- [处理 IRP](handling-irps.md) 介绍内核模式驱动程序如何处理 I/O 请求数据包 (IRP)。

- 直接内存访问 (DMA) 是驱动程序开发的一个重要方面，[本节点中的各主题](introduction-to-adapter-objects.md)涵盖了从 A 到 Z 的 DMA。

- [控制器对象](introduction-to-controller-objects.md)表示包含附加设备的物理设备控制器。

- [中断服务例程 (ISR)](introduction-to-interrupt-service-routines.md) 为接收中断的物理设备的驱动程序处理中断。

- [消息信号中断](introduction-to-message-signaled-interrupts.md)通过将值写入特定内存地址来触发中断。

- [延迟的过程调用（DPC 对象）](introduction-to-dpc-objects.md)可从 ISR 排队，并稍后以比 ISR 更低的 IRQL 执行。

- [即插即用 (PnP)](introduction-to-plug-and-play.md) 侧重于针对 PnP 的系统软件支持以及驱动程序如何使用该支持来实现 PnP。

- [电源管理](introduction-to-power-management.md)介绍了一种为系统和设备电源管理提供全面方法的体系结构。

- [Windows Management Instrumentation (WMI)](implementing-wmi.md) 是内核模式驱动程序的扩展，使你的驱动程序能够成为一个 WMI 提供程序。 WMI 提供程序使度量和检测数据可用于 WMI 使用者，如用户模式应用程序。

- [驱动程序编程技术](using-nt-and-zw-versions-of-the-native-system-services-routines.md)；在 Windows 内核模式下对驱动程序进行编程所需的技术有时与普通用户模式编程所需的技术有很大不同。
