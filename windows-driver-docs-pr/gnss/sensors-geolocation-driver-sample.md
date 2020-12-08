---
title: Windows 8.1 的地理位置驱动程序示例
description: Windows 8.1 的地理位置示例驱动程序演示了全球定位系统 (GPS) 设备的传感器驱动程序。
keywords:
- GPS
- 地理位置驱动程序
- GPS 驱动程序
- 收音机管理 API
- 无线电-状态更改
- 传感器驱动程序
- UMDF 传感器驱动程序
ms.date: 08/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: e90d6c54dd2aca1362b55d3ea12cae179625ce4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819081"
---
# <a name="geolocation-driver-sample-for-windows-81"></a>Windows 8.1 的地理位置驱动程序示例

> [!IMPORTANT]
> 此文档和 Windows 8.1 的地理位置驱动程序示例已弃用。

Windows 8.1 的地理位置示例驱动程序演示了全球定位系统 (GPS) 设备的传感器驱动程序。 此驱动程序不连接到硬件;否则，它完全符合生成 UMDF 传感器驱动程序的最佳做法。 此示例模拟一个传感器，该传感器发出海拔、纬度、经度和其他模拟 GPS 数据，而不是发送实际的坐标。 此外，此示例还会发出一个在测试和调试时非常有用的时间戳。

此示例有三个用途：首先，它演示了 UMDF 传感器驱动程序所需的最小功能。 其次，它提供了一个可用于构建工作驱动程序的主干。 第三，它包括对收音机管理 API 的支持，此 API 提供对设备（如 GPS）的无线电状态更改的通知。

## <a name="related-topics"></a>相关主题

[传感器诊断工具](../sensors/the-sensor-diagnostic-tool.md)
  
[写入位置传感器驱动程序](writing-a-location-sensor-driver.md)
