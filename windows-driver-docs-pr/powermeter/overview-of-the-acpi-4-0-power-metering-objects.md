---
title: ACPI 4.0 功率计量对象概述
description: ACPI 4.0 功率计量对象概述
keywords:
- 电源计量和预算 WDK，ACPI 4.0 电源计量对象
- ACPI 4.0 电源计量对象 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3037461c495585a16ac29779fd131fb4e7fedd95
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794293"
---
# <a name="overview-of-the-acpi-40-power-metering-objects"></a>ACPI 4.0 功率计量对象概述


 (PMI) 的 ACPI 电源指示器接口向提供 WDM PMI 接口的驱动程序公开硬件平台的电源计量和预算功能。

ACPI PMI 由 ACPI 4.0 电源计量对象提供。 这些对象为硬件平台提供了用于电源计量和预算的协议的抽象层。 此抽象层为所有硬件平台上的操作系统提供了一个一致的电源和计量接口。

系统固件必须实现 ACPI 4.0 电源计量对象。 平台实现细节是专有的，特定于系统。

符合 PMI 标准的电源和计量通过 ACPI 硬件 ID "ACPI000D" 进行标识。 此外，ACPI PMI 定义用于获取静态信息的控制方法，并用于查询或设置动态信息。 例如，使用 ACPI PMI 控制方法从符合 PMI 标准的电源指示器中读取当前功率。

PMI 事件（例如，超过电源阈值时）通过电源指示器设备上的一组 ACPI 通知代码发出信号。

每个 ACPI PMI 命名空间对象都具有适当的控制方法，可允许在操作系统与硬件平台之间进行交互。 这些控制方法提供对以下各项的支持：

-   电源和电源指示器的查询。

-   查询运行时功率消耗度量值。

-   通过电源指示器管理电源预算。

-   事件通知。

 

 




