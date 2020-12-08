---
title: Power 框架 (PoFx) 驱动程序示例
description: 此目录中的驱动程序示例提供了为设备编写自定义 PoFx 驱动程序的起点。
ms.date: 11/19/2019
ms.localizationpriority: medium
ms.openlocfilehash: 2583d38209665e96a45d1db55901ffaf0cfa1dd0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785607"
---
# <a name="power-framework-pofx-driver-samples"></a>Power 框架 (PoFx) 驱动程序示例

此目录中的驱动程序示例提供了为设备编写自定义 PoFx 驱动程序的起点。

| 示例 | 说明 |
| --- | --- |
| [PEP ACPI 示例](/samples/microsoft/windows-driver-samples/pep-acpi-sample) | 演示一个接口，该接口允许 Power Engine 插件 (PEP) 通过 Windows 驱动程序而不是固件实现本地 ACPI 运行时方法。 |
| [UMDF2 PoFx 驱动程序](/samples/microsoft/windows-driver-samples/power-framework-pofx-sample-umdf-version-2) | UMDF 2 SingleComp 示例演示了 UMDF2 驱动程序如何为只有单个组件的设备实现基于 F 状态的电源管理。 |
| [WDF PoFx 驱动程序](/samples/microsoft/windows-driver-samples/kmdf-power-framework-pofx-sample) | 包含两个示例，演示 KMDF 驱动程序如何实现基于 F 状态的电源管理。 SingleComp 示例演示了 KMDF 驱动程序如何为只有单个组件的设备实现基于 F 状态的电源管理。 MultiComp 示例演示了 KMDF 驱动程序如何为具有任意数量的组件（可以单独进行电源管理）的设备实现基于 F 状态的电源管理 |
