---
title: ACPI 4.0 功率计量对象概述
description: ACPI 4.0 功率计量对象概述
ms.assetid: 91488b88-bbdc-40e9-9095-2ea3fb7d69ad
keywords:
- Power 计量和预算 WDK，ACPI 4.0 power 计数对象
- ACPI 4.0 能源计量对象 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f03bd14336c5fddca298b6f7775ef8114bf4d161
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381260"
---
# <a name="overview-of-the-acpi-40-power-metering-objects"></a>ACPI 4.0 功率计量对象概述


ACPI Power 计量接口 (PMI) 公开 power 计量和预算提供 WDM PMI 接口的驱动程序的硬件平台的功能。

ACPI PMI 由 ACPI 4.0 能源计量对象提供。 这些对象提供抽象层，以使用的硬件平台 power 计量和预算的协议。 此抽象层提供了一致电源和计量接口对操作系统跨所有硬件平台。

系统固件必须实现 ACPI 4.0 能源计量对象。 平台实现详细信息具有专有性和特定于系统。

电源和 PMI 合规的计量器通过"ACPI000D"ACPI 硬件 ID 进行标识。 此外，ACPI PMI 定义用于获取静态信息，并查询或设置动态控制方法的信息。 例如，ACPI PMI 控件方法被定义为从 PMI 符合电表读取当前的功耗。

PMI 事件，如 power 超出阈值，将通过一系列 ACPI 收到信号时通知 power 测定仪设备上的代码。

ACPI PMI 命名空间的每个对象具有相应的控件允许操作系统和硬件平台之间的交互的方法。 这些控制方法提供以下支持：

-   电源和功耗计量特征的查询。

-   运行时电源消耗测量结果的查询。

-   管理电源预算的电源表。

-   事件通知。

 

 




