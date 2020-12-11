---
title: 设备和驱动程序安装概述
description: 设备和驱动程序安装概述
keywords:
- 设备安装程序 WDK 设备安装 , 关于设备安装
- 设备安装 WDK , 关于设备安装
- 安装设备 WDK , 关于设备安装
ms.date: 10/16/2019
ms.localizationpriority: High
ms.openlocfilehash: 2b340dc8aeeb3a754897527dfc635dc23e41de20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793597"
---
# <a name="overview-of-device-and-driver-installation"></a>设备和驱动程序安装概述

当系统重新启动或用户插入（或手动安装）即插即用 (PnP) 设备时，Windows 操作系统将安装设备。

具体而言，Windows 会枚举系统中存在的设备，并为每个设备加载并调用驱动程序。

诸如 ACPI 驱动程序和其他 PnP [总线驱动程序](../kernel/bus-drivers.md)之类的驱动程序将帮助 Windows 确定哪些设备存在。

## <a name="in-this-section"></a>本部分内容


-   [步骤 1：标识新设备](step-1--the-new-device-is-identified.md)
-   [步骤 2：选择设备的驱动程序](step-2--a-driver-for-the-device-is-selected.md)
-   [步骤 3：安装设备的驱动程序](step-3--the-driver-for-the-device-is-installed.md)
-   [驱动程序选择过程概述](overview-of-the-driver-selection-process.md)
