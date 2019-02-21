---
title: 能源计量和预算方面的基础结构概述
description: 能源计量和预算方面的基础结构概述
ms.assetid: eda1c829-eb5e-404b-bf6b-1b0807ee02c7
keywords:
- Power 计量和预算 WDK 概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaeef30d377b47a548a5bb159c00173e995bc017
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533771"
---
# <a name="overview-of-the-power-metering-and-budgeting-infrastructure"></a>能源计量和预算方面的基础结构概述


从 Windows 7 和 Windows Server 2008 R2 开始，Windows 支持的能源计量和预算 (PMB) 基础结构。 此基础结构将在计算机系统的能源效率提升通过提供电源使用情况和管理功能。 此外，PMB 提供配置其他选项 power 计量和预算。 系统制造商、 IT 专业人员和最终用户可以使用 PMB 基础结构优化他们的系统，以便以满足其需求的能力和性能之间进行平衡。

PMB 基础结构提供了对用户模式应用程序和服务的以下信息：

<span id="Power_Metering_Information"></span><span id="power_metering_information"></span><span id="POWER_METERING_INFORMATION"></span>电源计数信息  
此信息用于确定计算机系统或子组件如何使用电源。 监视电源消耗，或*按流量计费的*，通过在系统中的 power 计量。 能源计量还提供了电源表，如功能和电源消耗阈值计数的当前配置。

<span id="Power_Budgeting_Information"></span><span id="power_budgeting_information"></span><span id="POWER_BUDGETING_INFORMATION"></span>电源预算方面的信息  
使用此信息来确定 power 限制，或*预算*，即支持的计算机系统。 具体取决于硬件平台，此信息可能还允许您配置系统的功率消耗。

电源表是报告有关功率消耗，以瓦为单位的信息系统的硬件组件。 通常作为的一部分的电源或通过基板管理控制器 (BMC) 提供此信息。 电源指示器监视整个系统的功率消耗或的计算机的子系统和生成事件 （如果已配置为执行此操作） 出现以下条件之一：

-   功率消耗超出配置的电源阈值的电源。

-   系统消耗的功率达到配置的电源预算。

无法在计算机系统中，安装多个电表，与每个电表，监视其自己的组件集。

下图概述 PMB 基础结构。

![能源计量和预算 (pmb) 基础结构的关系图概述 ](images/powermeter-1.png)

PMB 由以下组件构成：

<span id="User-Mode_Power_Service__UMPS_"></span><span id="user-mode_power_service__umps_"></span><span id="USER-MODE_POWER_SERVICE__UMPS_"></span>用户模式下 Power 服务 (UMPS)  
UMPS 是通过使用 WMI 类的一组用户模式服务公开系统的能源计量和预算方面的信息。 应用程序，如 Windows 性能监视器 (PerfMon)，使用此信息有关电源管理和报告。

由 UMPS 电源 WMI 提供程序组件提供了 PMB WMI 类。 这些 WMI 类符合版本*1.1.0 分布式管理任务组 (DMTF) 电源提供配置文件*。 有关详细信息，请参阅[DMTF 电源提供配置文件](https://go.microsoft.com/fwlink/p/?linkid=145048)。

有关 UMPS 详细信息，请参阅[用户模式下 Power 服务](user-mode-power-service.md)。

<span id="Power_Meter_Interface__PMI__"></span><span id="power_meter_interface__pmi__"></span><span id="POWER_METER_INTERFACE__PMI__"></span>电源指示器接口 (PMI)   
PMI 是驱动程序提供一个 WDM 接口。 通过使用此接口，该驱动程序 PMI I/O 请求数据包 (Irp) 服务从[电源管理器](https://msdn.microsoft.com/library/windows/hardware/ff559829)和 UMPS 电源 WMI 提供程序组件。 这些 Irp 用于查询和设置的当前能源计量和预算方面的信息从电源表。

从 Windows 7 和 Windows Server 2008 R2 开始，操作系统提供了驱动程序 (*ACPIPMI。SYS*) 实现支持 ACPI 4.0 能源计量对象的系统的 PMI。 此驱动程序，原始设备制造商 (Oem) 可以构建可参与 PMB 基础结构中，而无需安装第三方驱动程序的系统。

有关 PMI 详细信息，请参阅[电源计量接口](power-meter-interface.md)。

<span id="ACPI_PMI"></span><span id="acpi_pmi"></span>ACPI PMI  
ACPI PMI 公开 power 计量和预算提供 WDM PMI 接口的驱动程序的硬件平台的功能。

ACPI PMI 是通过使用 ACPI 4.0 能源计量对象提供。 这些 ACPI 对象提供抽象层的基础技术，如智能平台管理接口 (IPMI)，是用于进行计量和预算的电源的硬件平台。

ACPI 4.0 能源计量对象被模仿 ACPI 控件方法电池范例。 系统固件必须实现 ACPI 4.0 能源计量对象。 系统固件还必须实现 ACPI 4.0 能源计量对象。 实现详细信息具有专有性和特定于每个系统。

有关详细信息，请参阅[ACPI 电源计量接口](acpi-power-meter-interface.md)。

 

 




