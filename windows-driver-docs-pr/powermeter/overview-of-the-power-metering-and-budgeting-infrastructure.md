---
title: 功率计量和预算基础结构概述
description: 功率计量和预算基础结构概述
keywords:
- 能源测定和预算 WDK，概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 928ce92a3722a5a25e2d8f928bf9e6d273bc6941
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812475"
---
# <a name="overview-of-the-power-metering-and-budgeting-infrastructure"></a>功率计量和预算基础结构概述


从 Windows 7 和 Windows Server 2008 R2 开始，Windows 支持 PMB) 基础结构的电源计量和预算 (。 此基础结构通过提供功率消耗和管理功能提高了计算机系统的能源效率。 此外，PMB 还提供了用于配置电源计量和预算的其他选项。 系统制造商、IT 专业人员和最终用户可以使用 PMB 基础结构来优化其系统，以便能够平衡电源和性能以满足其需求。

PMB 基础结构为用户模式应用程序和服务提供以下信息：

<span id="Power_Metering_Information"></span><span id="power_metering_information"></span><span id="POWER_METERING_INFORMATION"></span>电源计量信息  
此信息用于确定计算机系统或子组件如何使用电源。 电源消耗按系统中的电源指示器进行监视或 *计量*。 电源计量还提供电源指示器的当前配置，例如计量功能和功率消耗阈值。

<span id="Power_Budgeting_Information"></span><span id="power_budgeting_information"></span><span id="POWER_BUDGETING_INFORMATION"></span>能源预算信息  
此信息用于确定计算机系统支持的电源限制（或 *预算*）。 根据硬件平台，此信息还可能允许配置系统的功率消耗。

电源指示器是系统的硬件组件，用于报告功率消耗的相关信息。 此信息通常作为电源或通过使用底板管理控制器 (BMC) 提供。 电源指示器监视整个系统或计算机子系统的能耗，并生成事件 (如果在发生以下情况之一时) 配置为执行此操作：

-   功率消耗超过电源的配置电源阈值。

-   系统消耗的电量达到配置的功率消耗。

可以在一台计算机系统中安装多个电源计量，每个电源指示器都监视其自己的一组组件。

下图概述了 PMB 基础结构。

![电源计量和预算 (pmb) 基础结构的关系图概述 ](images/powermeter-1.png)

PMB 包含以下组件：

<span id="User-Mode_Power_Service__UMPS_"></span><span id="user-mode_power_service__umps_"></span><span id="USER-MODE_POWER_SERVICE__UMPS_"></span>用户模式电源服务 (UMPS)   
UMPS 是一种用户模式服务，它使用一组 WMI 类公开系统的电源计量和预算信息。 此信息由应用程序使用，例如 Windows 性能监视器 (PerfMon) ，用于电源管理和报告。

PMB WMI 类由 UMPS 的 Power WMI Provider 组件提供。 这些 WMI 类符合 *分布式管理任务组 (DMTF) 电源配置文件的版本 1.1.0*。 有关详细信息，请参阅 [DMTF 电源配置文件](https://go.microsoft.com/fwlink/p/?linkid=145048)。

有关 UMPS 的详细信息，请参阅 [用户模式电源服务](user-mode-power-service.md)。

<span id="Power_Meter_Interface__PMI__"></span><span id="power_meter_interface__pmi__"></span><span id="POWER_METER_INTERFACE__PMI__"></span> (PMI) 的电源指示器接口   
PMI 是由驱动程序提供的 WDM 接口。 通过使用此接口，驱动程序服务 PMI i/o 请求数据包 (Irp) 来自 UMPS 的 [Power Manager](../kernel/power-manager.md) 和 Power WMI 提供程序组件。 这些 Irp 用于查询和设置电源指示器的当前电源计量和预算信息。

从 Windows 7 和 Windows Server 2008 R2 开始，操作系统提供了一个 (*ACPIPMI.SYS*) 的驱动程序，该驱动程序为支持 ACPI 4.0 电源计量对象的系统实现 PMI。 此驱动程序使 Oem)  (Oem 可以在无需安装第三方驱动程序的情况下生成可参与 PMB 基础结构的系统。

有关 PMI 的详细信息，请参阅 [电源指示器界面](power-meter-interface.md)。

<span id="ACPI_PMI"></span><span id="acpi_pmi"></span>ACPI PMI  
ACPI PMI 向提供 WDM PMI 接口的驱动程序公开硬件平台的电源计量和预算功能。

ACPI PMI 是使用 ACPI 4.0 电源计量对象提供的。 这些 ACPI 对象为底层技术提供抽象层，如智能平台管理接口 (IPMI) ，用于通过硬件平台进行电源计量和预算。

ACPI 4.0 电源计量对象在 ACPI 控制方法电池模式后建模。 系统固件必须实现 ACPI 4.0 电源计量对象。 系统固件还必须实现 ACPI 4.0 电源计量对象。 实现细节是专有的，并特定于每个系统。

有关详细信息，请参阅 [ACPI Power 计量接口](acpi-power-meter-interface.md)。

 

