---
title: Windows 硬件错误体系结构定义
description: Windows 硬件错误体系结构定义
keywords:
- Windows 硬件错误体系结构 WDK，术语
- WHEA WDK，术语
- 硬件错误 WDK WHEA，术语
- 错误 WDK WHEA，术语
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f453a98890c98b6335e062c1b3a0fe9430bb2bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838699"
---
# <a name="windows-hardware-error-architecture-definitions"></a>Windows 硬件错误体系结构定义


下面是与 Windows 硬件错误体系结构 (WHEA) 相关的术语的定义。

<a href="" id="advanced-configuration-and-power-interface--acpi-"></a>高级配置和电源接口 (ACPI)  
适用于操作系统定向设备配置和电源管理的行业标准接口。 有关 ACPI 的详细信息，请参阅 [Acpi 规范](https://uefi.org/sites/default/files/resources/ACPI_6_3_final_Jan30.pdf)。

<a href="" id="baseboard-management-controller--bmc-"></a>基板管理控制器 (BMC)  
主板上管理特定于平台的功能（如监视和处理某些环境错误情况）的一组硬件组件。

<a href="" id="corrected-machine-check--cmc-"></a>更正了计算机检查 (CMC)   
由硬件或固件纠正的处理器检测到的错误条件。 通常会通过以下方式向操作系统报告 CMC：发送中断，或在操作系统定期轮询的错误注册中设置位。 这是一个非致命错误情况。

<a href="" id="corrected-platform-error--cpe-"></a>更正了平台错误 (CPE)   
由硬件或固件纠正的平台硬件检测到的错误条件。 通常会通过发出中断的信号或在由操作系统定期轮询的错误寄存器中设置位来向操作系统报告 CPE。 这是一个非致命错误情况。

<a href="" id="event-log--el-"></a>事件日志 (EL)   
跟踪系统组件上发生的事件的 Windows 操作系统组件。 WHEA 使用系统事件日志来记录硬件错误事件。

<a href="" id="event-tracing-for-windows--etw-"></a>Windows 事件跟踪 (ETW)  
ETW 使软件开发人员能够启动和停止事件跟踪会话，检测应用程序以提供跟踪事件，并使用跟踪事件。 WHEA 使用 ETW 通知订户有关硬件错误事件，并在系统事件日志中记录硬件错误事件。

<a href="" id="extensible-firmware-interface--efi-"></a>可扩展固件接口 (EFI)  
操作系统和平台固件之间的接口的下一代模型。 此接口包含包含与平台相关的信息的数据表，以及可用于操作系统及其加载程序的启动和运行时服务调用。 它们共同提供了用于启动操作系统和运行预启动应用程序的标准环境。 有关 EFI 的详细信息，请参阅 [统一可扩展固件接口 (UEFI) 规范](https://go.microsoft.com/fwlink/p/?linkid=69484)。

<a href="" id="intelligent-platform-management-interface--ipmi-"></a>智能平台管理接口 (IPMI)   
用于监视和管理功能并内置于硬件平台中的接口。 IPMI 主要用于监视系统硬件的运行状况，并处理环境错误情况。 有关 IPMI 的详细信息，请参阅 [Ipmi 规范](https://go.microsoft.com/fwlink/p/?linkid=69485)。

<a href="" id="low-level-hardware-error-handler--llheh-"></a>低级别硬件错误处理程序 (LLHEH)   
为响应硬件错误条件而运行的第一个操作系统代码。 LLHEH 可以是中断处理程序、异常处理程序、轮询例程或系统固件调用的回调例程。 所有 LLHEHs 通过常见硬件错误报告功能向操作系统报告硬件错误。

<a href="" id="machine-check-abort--mca-"></a>计算机检查中止 (MCA)   
一种例外情况，即 Itanium 处理器向操作系统报告指示出现硬件错误。

<a href="" id="machine-check-architecture--mca-"></a>计算机检查体系结构 (MCA)   
用于向操作系统报告硬件错误的硬件和软件体系结构。

<a href="" id="machine-check-exception--mce-"></a>计算机检查异常 (MCE)   
X86 或 x64 处理器向操作系统报告指示出现硬件错误的异常。

<a href="" id="machine-specific-register--msr-"></a> (MSR) 的计算机特定寄存器  
系统软件用于实现某些功能的特定于处理器的寄存器。 每个 MSR 的操作都是特定于每个处理器和/或处理器系列的。

<a href="" id="nonmaskable-interrupt--nmi-"></a>不可屏蔽中断 (NMI)   
处理器向操作系统报告的中断，而不考虑处理器的当前中断优先级别。 当平台检测到致命硬件错误情况时，NMI 通常会发出信号。

<a href="" id="pci-express-advanced-error-reporting--pcie-aer-"></a>PCI Express 高级错误报告 (PCIe AER)   
PCI Express 的可选扩展功能，提供比标准 PCI Express 错误报告机制更强大的错误报告功能。 有关 PCIe AER 的详细信息，请参阅 [PCI Express 规范](https://go.microsoft.com/fwlink/p/?linkid=69486)。

<a href="" id="platform-specific-hardware-error-driver--pshed-"></a>平台特定的硬件错误驱动程序 (PSHED)   
提供基础平台硬件错误报告功能的抽象的 WHEA 组件。 Microsoft 为每个处理器体系结构提供了 PSHEDs。 平台供应商可以通过实现利用特定于平台的功能的 PSHED 插件来补充 PSHED 功能。

<a href="" id="service-control-interrupt--sci-"></a>服务控制中断 (科幻)   
ACPI 驱动程序处理的中断。 收到科幻后，ACPI 驱动程序将确定哪个设备发出了中断信号，然后对设备作出相应的响应。

<a href="" id="service-processor--sp-"></a>服务处理器 (SP)   
与主处理器 () 不同的微控制器，它管理特定于平台的功能，如监视环境条件和处理某些错误条件。 服务处理器通常是基板管理控制器硬件的一个组件。

 

 




