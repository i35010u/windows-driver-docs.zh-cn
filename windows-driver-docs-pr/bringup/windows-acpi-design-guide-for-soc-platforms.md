---
title: SoC 平台的 Windows ACPI 设计指南
description: ACPI 5.0 定义新功能，以支持基于 SoC ICs （实现连接待机电源模式）的低功耗移动设备。
ms.assetid: 661BFB7E-D190-450D-A466-7D6AD0EAAAB0
ms.date: 05/26/2020
ms.localizationpriority: medium
ms.openlocfilehash: 34c5b56cf914bb0ce8e241621020c21bf8a6cade
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186505"
---
# <a name="windows-acpi-design-guide-for-soc-platforms"></a>SoC 平台的 Windows ACPI 设计指南

高级配置和电源接口规格 5.0 修正版（[ACPI 5.0 规格](https://uefi.org/specifications)）定义了一组新的功能，这些功能可以支持低功耗的移动设备，而这些移动设备则基于系统单芯片 (SoC) 集成电路并实现了连接待机电源模型。 从 Windows 8 和 Windows 8.1 开始，Windows 支持基于 SoC 的平台的新 ACPI 5.0 功能。

本部分包含有关实现支持 ACPI 5.0 规范中新功能的 Windows 电脑和设备的指南。 固件开发人员和系统设计人员可以使用这些准则来确保 Windows 在其平台上正常运行。 有关所有 Windows 固件要求的列表，请参阅 [Windows 认证计划](/previous-versions/windows/hardware/hck/jj124227(v=vs.85))的文档。

## <a name="in-this-section"></a>在本节中

| 主题 | 说明 |
| --- | --- |
| [针对 ACPI 5.0 的 Windows 支持概述](overview-of-windows-support-for-acpi-5-0.md) | [ACPI 5.0 规范](https://uefi.org/specifications)支持在 windows 8 及更高版本中运行的基于 SoC 的移动平台，但继续支持在早期版本的 windows 中引入的许多有用功能。 此设计指南将实施者指引到专门适用于基于 SoC 的平台的 ACPI 5.0 的各个部分，并介绍在 ACPI 中实现特定于 SoC 的功能以在这些平台上运行 Windows 的最佳实践。 |
| [ACPI 系统说明表](acpi-system-description-tables.md) | 支持高级配置和电源接口 (ACPI) 硬件规范在基于 Windows Server 的基于 SoC 的平台或 Windows Server 系统上不是必需的，但很多 ACPI 软件规范都是 (或) 必需的。 ACPI 定义了一个通用的可扩展表传递机制，还定义了用于为操作系统描述平台的特定表。 |
| [设备管理命名空间对象](device-management-namespace-objects.md) | [ACPI 5.0 规范](https://uefi.org/specifications)定义了几种可用于管理设备的命名空间对象类型。 例如，设备标识对象包含连接到总线的设备的标识信息，例如 I2C，不支持子设备的硬件枚举。 其他类型的命名空间对象可以指定系统资源、描述设备依赖关系，并指明哪些设备可以禁用。 |
| [常规用途 I/O (GPIO)](general-purpose-i-o--gpio-.md) | SoC 集成线路广泛使用了常规用途 i/o (GPIO) 针。 对于基于 SoC 的平台，Windows 定义了 GPIO 硬件的常规抽象，此抽象需要 (ACPI) 命名空间的高级配置和电源接口支持。 |
| [简单的外围总线 (SPB) ](simple-peripheral-bus--spb-.md) | SoC 集成线路广泛使用简单、低 pin 计数和低功耗串行互连，以便连接到平台外围设备。 例如，UARTs。 对于基于 SoC 的平台，Windows 为简单的外围总线 (SPB) 硬件提供常规抽象，此抽象需要高级配置和电源接口 (ACPI) 命名空间中的新支持。 |
| [设备电源管理](device-power-management.md) | [ACPI 5.0 规范](https://uefi.org/specifications)定义一组命名空间对象，以指定设备的设备电源信息。 例如，一组对象可以指定设备在每个受支持的设备电源状态下所需的电源资源。 另一种对象类型可以描述设备从低功耗状态唤醒以响应硬件事件的能力。 |
| [ACPI 定义的设备](acpi-defined-devices.md) | [ACPI 5.0 规范](https://uefi.org/specifications)定义了许多用于表示和控制典型平台功能的设备类型。 例如，ACPI 定义 "电源" 按钮、"睡眠" 按钮和 "系统指示器"。 对于基于 SoC 的平台，Windows 提供内置驱动程序来支持本文中所述的 ACPI 定义的设备。 |
| [其他 ACPI 命名空间对象](other-acpi-namespace-objects.md) | 对于某些特定类别的设备，需要提供额外的高级配置和电源接口 (ACPI) 命名空间对象，使其出现在命名空间中的这些设备下。 本部分列出了基于 SoC 的平台所需的其他对象。 |
| [ACPI 的特定于设备的方法](acpi-device-specific-methods.md) | 为了支持增加的功能和扩展来选择技术堆栈，Windows 为设备定义了特定于设备的方法 (_DSM) 。 |