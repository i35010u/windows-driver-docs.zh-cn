---
title: 电源管理的全系统概述
description: 电源管理的全系统概述
ms.assetid: 16313152-3fe2-49d7-8cf1-b369e39e4130
keywords:
- 电源管理 WDK 内核，有关电源管理
- 电源管理 WDK 内核，整个系统概述
- 软件 WDK 电源管理
- 控件面板 WDK 电源管理
- 整个系统电源策略 WDK 内核
- 电源策略 WDK 内核
- 节省电源 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17a37a25eeeb490176b3736aa12030fb20f0ce15
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345415"
---
# <a name="system-wide-overview-of-power-management"></a>电源管理的全系统概述





电源管理需要从系统和设备的硬件和系统软件和驱动程序的支持。 在上一部分中所述在行业规范中，介绍了所需的硬件支持。 本主题介绍软件支持 — 具体而言，驱动程序必须做什么来符合操作系统要求以及管理根据他们的设备的电源。

下图显示了电源管理的系统级概述。

![说明电源管理的系统级概述关系图](images/power-comp.png)

应用程序和用户可能会影响通过控制面板和通过调用电源管理例程的电源管理决策。 用户可以使用控制面板设置系统和设备电源选项，包括自定义电源设置。 控制面板通知的电源管理器和活动的电源策略及其关联的电源设置发生更改的驱动程序。 从 Windows Vista 开始，电源管理器会通知驱动程序通过调用[**电源设置回调**](https://msdn.microsoft.com/library/windows/hardware/ff559727)驱动程序注册以接收通知。 在 Windows Server 2003、 Windows XP 和 Windows 2000 中，通过 WMI 执行此通知。

电源管理器管理系统级*电源策略*，规则来控制系统的电源使用情况。 (有关详细信息，请参阅[系统电源策略](system-power-policy.md)。)使用控制面板和 Api 中的信息，电源管理器可以确定当应用程序使用的，或者可能需要使用各种设备，以便它可以相应地调整系统的电源策略。

电源管理器还提供了一个接口驱动程序，请包含[电源管理支持例程](https://msdn.microsoft.com/library/windows/hardware/ff559835)，[电源管理次要 Irp](https://msdn.microsoft.com/library/windows/hardware/ff559822)，和所需驱动程序入口点。

当电源管理器请求的系统电源状态更改时，驱动程序通过将其设备放在适当的设备电源状态响应。 此外，驱动程序可以为其设备执行空闲检测和未使用的设备置于睡眠状态。 特定于总线的机制报告设备电源功能、 设置和报告设备状态和更改设备电源。 完全如何以及何时更改设备电源取决于设备的类型和设备硬件的功能。

ACPI 硬件意识到最大电源节省量，尽管硬件不需要符合 ACPI 才能有效的驱动程序中的电源管理的。

 

 




