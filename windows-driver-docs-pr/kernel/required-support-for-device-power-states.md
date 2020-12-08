---
title: 设备电源状态所需的支持
description: 设备电源状态所需的支持
keywords:
- 持续电能 WDK 内核
- 延迟 WDK 电源管理
- 设备电源状态 WDK 内核
- 硬件 WDK 电源管理
- 传统电源管理 WDK 内核
- 类驱动程序 WDK 电源管理
- 端口驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c34378e218ccdb6923d660ba7eac8c5ed71a017
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820657"
---
# <a name="required-support-for-device-power-states"></a>设备电源状态所需的支持





请参阅相关的设备类电源管理参考规范，查明为你使用的设备类定义了哪些设备电源状态以及每种状态的操作要求。 这些规范可在 [ACPI/电源管理](https://go.microsoft.com/fwlink/p/?linkid=57185) 网站上找到。

不存在电源管理规范的旧式设备和其他设备应遵循默认的设备类电源管理规范。 默认规范要求：

-   支持 D0 和 D3 状态。

-   驱动程序，用于在设备打开时保存和还原或重新初始化设备上下文。

-   管理设备电源策略的驱动程序。

与系统一起提供的类和端口驱动程序以及独立的硬件供应商 (Ihv) 通常支持电源管理。 如果要编写链接到此类驱动程序的微型驱动程序，请在 Windows 驱动程序工具包 (WDK) 中查看相关的类或端口驱动程序文档，以了解微型驱动程序中所需的电源管理支持范围。 以下一般准则适用：

-   网络适配器驱动程序必须符合网络驱动程序接口规范 6.00 (NDIS 6.0)  (Windows Vista) 或 NDIS 5.0 (Windows Server 2003、Windows XP 和 Windows 2000) 。 此外，驱动程序必须符合驱动程序的设备安装程序类的电源管理要求和驱动程序的 Windows 版本。

-   流式处理驱动程序使用流式处理类驱动程序中的电源管理界面来处理设备电源状态 D0 和 D3。 若要处理设备电源状态 D1 和 D2，这些驱动程序必须使用本节中所述的电源管理接口。

-   SCSI 端口驱动程序管理微型端口的大多数 PnP 和电源管理要求。 SCSI 微型端口驱动程序必须支持 PnP 和电源管理接口以及相关的例程（如 [**HwScsiAdapterControl**](/previous-versions/windows/hardware/drivers/ff557274(v=vs.85))）。

-   视频端口驱动程序管理微型端口的大多数 PnP 和电源管理要求。 视频微型端口驱动程序必须支持特定于微型端口的例程，该例程在 WDK 中的其他地方进行了介绍。

 

