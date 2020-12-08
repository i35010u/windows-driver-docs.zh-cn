---
title: 电源管理的全系统概述
description: 电源管理的全系统概述
keywords:
- 电源管理 WDK 内核，关于电源管理
- 电源管理 WDK 内核，系统范围的概述
- 软件 WDK 电源管理
- 控制面板 WDK 电源管理
- 系统范围电源策略 WDK 内核
- 电源策略 WDK 内核
- 保存电源 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e8fe04ab8b99c81a2fb14f7aec28d7ecc30a96cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827021"
---
# <a name="system-wide-overview-of-power-management"></a>电源管理的全系统概述





电源管理需要系统和设备硬件以及系统软件和驱动程序的支持。 如前一部分中所述，行业规范中涵盖了所需的硬件支持。 本主题涵盖软件支持：具体而言，软件支持必须执行哪些操作才能符合操作系统要求并针对其设备管理电源。

下图显示了系统范围内电源管理的概述。

![阐释系统范围内电源管理概述的示意图](images/power-comp.png)

应用程序和用户可以通过 "控制面板" 和 "调用电源管理" 例程来影响电源管理决策。 用户可以使用 "控制面板" 设置系统和设备电源选项，包括自定义电源设置。 控制面板通知电源管理器和驱动程序活动电源策略和相关电源设置的更改。 从 Windows Vista 开始，电源管理器通过调用驱动程序注册接收通知的 [**电源设置回调**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-poregisterpowersettingcallback) 来通知驱动程序。 在 Windows Server 2003、Windows XP 和 Windows 2000 中，此通知通过 WMI 进行。

电源管理器管理系统范围内的 *电源策略*，这是控制系统电源使用情况的规则。  (有关详细信息，请参阅 [系统电源策略](system-power-policy.md)。 ) 使用控制面板和 api 中的信息，电源管理器可以确定应用程序使用的时间，或可能需要使用各种设备的时间，以便它能够相应地调整系统的电源策略。

Power manager 还为驱动程序提供了一个接口，其中包含 [电源管理支持例程](/windows-hardware/drivers/ddi/index)、 [电源管理辅助 irp](./power-management-minor-irps.md)和所需的驱动程序入口点。

当电源管理器请求对系统电源状态的更改时，驱动程序会通过将其设备置于适当的设备电源状态来做出响应。 此外，驱动程序可以为其设备执行空闲检测并将未使用的设备置于睡眠状态。 特定于总线的机制报告设备电源功能、设置和报告设备状态以及更改设备电源。 设备电源发生变化的确切方式和时间取决于设备的类型和设备硬件的功能。

尽管 ACPI 硬件可以实现最大的节能，但硬件不需要满足 ACPI 要求，驱动程序中的电源管理才能生效。

 

