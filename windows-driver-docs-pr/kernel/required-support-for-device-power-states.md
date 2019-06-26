---
title: 设备电源状态所需的支持
description: 设备电源状态所需的支持
ms.assetid: f7218f2a-d4ad-4b9a-af90-057801e714a2
keywords:
- 连续 power WDK 内核
- 延迟 WDK 电源管理
- 设备电源状态 WDK 内核
- 硬件 WDK 电源管理
- 旧的电源管理 WDK 内核
- 类驱动程序 WDK 电源管理
- 端口驱动程序 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc14a78e34ca4e4cdc444b38ccb5db34d7335ca8
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373411"
---
# <a name="required-support-for-device-power-states"></a>设备电源状态所需的支持





请参阅相关设备类电源管理引用规范来找出哪些设备电源状态定义为与你正在使用和每个状态操作的要求是什么设备的类。 这些规范是网址[ACPI / 电源管理](https://go.microsoft.com/fwlink/p/?linkid=57185)网站。

传统的设备和无电源管理规范存在的其他设备应遵循默认设备类电源管理规范。 默认值规范要求：

-   支持的 D0 和 D3 状态。

-   保存和还原或重新初始化设备上下文，在打开设备时驱动程序。

-   管理设备电源策略驱动程序。

随系统提供的类和端口驱动程序，通过独立硬件供应商 (Ihv) 通常支持电源管理。 如果您编写微型驱动程序链接到此类驱动程序，检查相关的类或端口驱动程序文档中 Windows Driver Kit (WDK) 若要了解的微型驱动程序中所需的电源管理支持程度。 以下常规准则适用于：

-   网络适配器驱动程序必须符合网络驱动程序接口规范 6.00 (NDIS 6.0) (Windows Vista) 或 NDIS 5.0 （Windows Server 2003、 Windows XP 和 Windows 2000）。 此外，驱动程序必须符合的设备安装程序类的驱动程序和 Windows 版本的驱动程序的电源管理要求。

-   流式处理驱动程序使用的流式处理的类驱动程序中的电源管理接口来处理设备的电源状态 D0 和 D3。 若要处理设备的电源状态 D1 和 D2，这些驱动程序必须使用在本部分中所述的电源管理接口。

-   SCSI 端口驱动程序管理的微型端口的 PnP 和电源管理要求的大多数。 SCSI 微型端口驱动程序必须支持即插即用和电源管理接口以及相关的例程，如[ **HwScsiAdapterControl**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff557274(v=vs.85))。

-   视频端口驱动程序管理的微型端口的 PnP 和电源管理要求的大多数。 微型端口驱动程序必须支持特定于微型端口的例程，WDK 中其他地方所述。

 

 




