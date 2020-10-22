---
title: Windows 8.1 的新传感器功能和改进
description: 本主题概述了 WindowsWindows 8.1 中传感器的新增功能和改进。
ms.assetid: F52BC6D1-DF67-4DE7-BEEC-D18C2A90B4CF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6bb8c936a951473f5001997e31291e51b98a6978
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355995"
---
# <a name="new-sensor-features-and-improvements-for-windows-81"></a>Windows 8.1 的新传感器功能和改进


本主题概述了 WindowsWindows 8.1 中传感器的新增功能和改进。

## <a name="support-for-hid-devices"></a>支持 HID 设备


Windows 8.1 包括对在 HID 传输上运行的任何传感器的内置支持。 此支持由 HID 类驱动程序提供。

类驱动程序支持以下列表中的11个传感器：

-   三维加速度
-   环境光线
-   环境温度
-   大气力度
-   罗盘三维
-   设备方向
-   陀螺仪3D
-   湿度
-   倾斜仪3D
-   状态
-   邻近帮助

除了这11个传感器，HID 类驱动程序还支持自定义类，设备供应商可以使用它来支持未在列表中找到的任何传感器。

## <a name="testing-sensor-functionality-with-the-sensor-diagnostic-tool"></a>通过传感器诊断工具测试传感器功能


您可以使用传感器诊断工具来测试您的传感器驱动程序、固件和硬件。 [传感器诊断工具](the-sensor-diagnostic-tool.md)主题中介绍了此工具。

## <a name="sensor-driver-logic"></a>传感器驱动程序逻辑


新的编程指南包含一个描述传感器设备驱动程序的驱动程序逻辑的部分。 此逻辑表现为包括驱动程序初始化、驱动程序接口、驱动程序更新、设备更新和内部驱动程序方法的伪代码。 你将从 [传感器驱动程序逻辑](driver-logic--pseudo-code-.md) 主题开始了解此新部分。

## <a name="sensors-geolocation-driver-sample"></a>传感器地理位置驱动程序示例


地理位置示例驱动程序演示了模拟全球定位系统 (GPS) 设备的最小 UMDF 驱动程序。 新 [编程指南](/windows-hardware/drivers/gnss/installing-the-sample-driver)中详细介绍了此示例驱动程序。

地理位置示例驱动程序还包括的代码演示如何添加对收音机管理 API 的支持。 这在 [支持收音机管理](../gnss/supporting-radio-management.md) 主题中进行了介绍。

## <a name="related-topics"></a>相关主题

[传感器驱动程序逻辑](driver-logic--pseudo-code-.md)  
[传感器诊断工具](the-sensor-diagnostic-tool.md)