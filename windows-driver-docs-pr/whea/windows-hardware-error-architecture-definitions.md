---
title: Windows 硬件错误体系结构定义
description: Windows 硬件错误体系结构定义
ms.assetid: 4de5ead1-aa17-4c14-9afc-bc0d9689a13e
keywords:
- Windows 硬件错误体系结构 WDK 术语
- WHEA WDK 术语
- 硬件错误 WDK WHEA，术语
- 错误 WDK WHEA，术语
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 93a9ec87b9597d0461ba3ea687e7c9a2423d24a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533096"
---
# <a name="windows-hardware-error-architecture-definitions"></a>Windows 硬件错误体系结构定义


以下是相关的 Windows 硬件错误体系结构 (WHEA) 的术语的定义。

<a href="" id="advanced-configuration-and-power-interface--acpi-"></a>高级的配置和电源接口 (ACPI)  
用于操作系统定向的设备配置和电源管理的行业标准接口。 ACPI 的详细信息，请参阅[ACPI 规范](https://go.microsoft.com/fwlink/p/?linkid=69483)。

<a href="" id="baseboard-management-controller--bmc-"></a>基板管理控制器 (BMC)  
一组管理特定于平台的功能，如监视和处理某些环境错误条件母板上的硬件组件。

<a href="" id="corrected-machine-check--cmc-"></a>更正计算机检查 (CMC)  
已更正的硬件或固件处理器检测到错误条件。 通过发出信号中断或通过定期轮询由操作系统错误寄存器中设置位，CMC 通常会报告给操作系统。 这是一个非致命错误条件。

<a href="" id="corrected-platform-error--cpe-"></a>已更正的平台错误 (CPE)  
由硬件或固件已更正的平台硬件检测到错误条件。 通过发出信号中断或通过定期轮询由操作系统错误寄存器中设置位，CPE 通常会报告给操作系统。 这是一个非致命错误条件。

<a href="" id="event-log--el-"></a>事件日志 (EL)  
跟踪系统组件发生的事件是 Windows 操作系统组件。 WHEA 使用系统事件日志中记录硬件错误事件。

<a href="" id="event-tracing-for-windows--etw-"></a>Windows (ETW) 事件跟踪  
ETW 提供了软件开发人员能够启动和停止检测应用程序能够提供跟踪事件和使用跟踪事件的事件跟踪会话。 WHEA 使用 ETW 来通知有关的硬件错误事件的订阅者，并在系统事件日志中记录硬件错误事件。

<a href="" id="extensible-firmware-interface--efi-"></a>可扩展固件接口 (EFI)  
用于操作系统和平台固件之间的接口的下一代模型。 接口包含的数据包含与平台相关的信息，以及启动和运行时服务的调用，可供操作系统和其加载程序的表。 在一起，这些启动操作系统和运行预启动应用程序提供标准环境。 EFI 的详细信息，请参阅[统一可扩展固件接口 (UEFI) 规范](https://go.microsoft.com/fwlink/p/?linkid=69484)。

<a href="" id="intelligent-platform-management-interface--ipmi-"></a>智能平台管理接口 (IPMI)  
一个接口，用于监视和管理功能，以及内置的硬件平台。 IPMI 主要用于监视的系统硬件运行状况并处理环境错误条件。 有关 IPMI 的详细信息，请参阅[IPMI 规范](https://go.microsoft.com/fwlink/p/?linkid=69485)。

<a href="" id="low-level-hardware-error-handler--llheh-"></a>低级别的硬件错误处理程序 (LLHEH)  
第一个操作系统中运行代码的硬件错误条件。 LLHEH 可以中断处理程序、 异常处理程序、 轮询例程或由系统固件调用的回调例程。 所有 LLHEHs 都报告到常见的硬件错误报告函数通过操作系统的硬件错误。

<a href="" id="machine-check-abort--mca-"></a>计算机检查中止 (MCA)  
Itanium 处理器报告向操作系统指明硬件错误已发生异常。

<a href="" id="machine-check-architecture--mca-"></a>计算机检查体系结构 (MCA)  
硬件错误报告给操作系统使用的硬件和软件体系结构。

<a href="" id="machine-check-exception--mce-"></a>计算机检查异常 (MCE)  
X86 或 x64 处理器报告给操作系统来指出发生了硬件错误异常。

<a href="" id="machine-specific-register--msr-"></a>计算机特定寄存器 (MSR)  
系统软件用于实现某些功能特定于处理器的寄存器。 每个 MSR 的操作是特定于每个处理器和/或处理器系列。

<a href="" id="nonmaskable-interrupt--nmi-"></a>不可屏蔽的中断 (NMI)  
无论处理器的当前中断优先级级别是什么操作系统向报告处理器中断。 平台检测到致命硬件错误条件时 NMI 通常向发出信号。

<a href="" id="pci-express-advanced-error-reporting--pcie-aer-"></a>PCI Express 高级错误报告 (PCIe AER)  
PCI Express 的可选扩展的功能，提供更可靠的错误报告比标准 PCI Express 错误报告机制。 有关 PCIe AER 详细信息，请参阅[PCI Express 规范](https://go.microsoft.com/fwlink/p/?linkid=69486)。

<a href="" id="platform-specific-hardware-error-driver--pshed-"></a>特定于平台的硬件错误驱动程序 (PSHED)  
WHEA 组件，提供的硬件错误报告的基础平台功能的抽象。 Microsoft 提供 PSHEDs 了对于每个处理器体系结构。 平台供应商可以通过实现 PSHED 插件，充分利用特定于平台的功能来补充 PSHED 功能。

<a href="" id="service-control-interrupt--sci-"></a>服务控制中断 (SCI)  
处理的 ACPI 驱动程序中断。 收到名工商管理学博士，ACPI 驱动程序确定哪台设备收到中断信号状态，然后相应地响应设备。

<a href="" id="service-processor--sp-"></a>服务处理器 (SP)  
微型控制器，不同于主要的处理器，用于管理特定于平台的功能，如监视环境条件和处理某些错误条件。 服务处理器通常是基板管理控制器硬件组件。

 

 




