---
title: 新的传感器功能和改进的 Windows 8.1
description: 本主题总结了的新功能和改进 WindowsWindows 8.1 中的传感器。
ms.assetid: F52BC6D1-DF67-4DE7-BEEC-D18C2A90B4CF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7ec1985eaaeca713d1ea898fc2c8ebcef74a47cc
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330107"
---
# <a name="new-sensor-features-and-improvements-for-windows-81"></a>新的传感器功能和改进的 Windows 8.1


本主题总结了的新功能和改进 WindowsWindows 8.1 中的传感器。

## <a name="support-for-hid-devices"></a>HID 设备的支持


Windows 8.1 包括对任意传感器 HID 传输上运行的内置支持。 通过 HID 类驱动程序提供此支持。

类驱动程序支持以下列表中的 11 个传感器：

-   Accelerometer 3D
-   环境光线
-   环境温度
-   大气压力
-   Compass 3D
-   设备方向
-   陀螺仪 3D
-   湿度
-   倾斜仪 3D
-   状态
-   邻近感应

除了这 11 个传感器的 HID 类驱动程序支持设备供应商可以使用它来支持在列表中找不到任何传感器的自定义类。

## <a name="testing-sensor-functionality-with-the-sensor-diagnostic-tool"></a>使用传感器诊断工具测试传感器功能


传感器诊断工具可用于测试传感器驱动程序、 固件和硬件。 此工具中所述[传感器诊断工具](the-sensor-diagnostic-tool.md)主题。

## <a name="sensor-driver-logic"></a>传感器驱动程序逻辑


在新的编程指南包含描述传感器设备驱动程序的驱动程序逻辑的部分。 此逻辑以涵盖的伪代码： 驱动程序初始化、 驱动程序接口、 驱动程序更新、 设备更新和内部驱动程序的方法。 您会发现此新部分开头[传感器驱动程序逻辑](driver-logic--pseudo-code-.md)主题。

## <a name="sensors-geolocation-driver-sample"></a>传感器地理位置驱动程序示例


地理位置示例驱动程序演示了模拟全球定位系统 (GPS) 设备的最小 UMDF 驱动程序。 此示例驱动程序详细介绍了在新[编程指南](programming-guide.md)。

地理位置示例驱动程序还包括演示如何添加对单选管理 API 的支持的代码。 这中所述[支持单选管理](https://msdn.microsoft.com/library/windows/hardware/jj200337)主题。

## <a name="related-topics"></a>相关主题
[编程指南](programming-guide.md)  
[传感器驱动程序逻辑](driver-logic--pseudo-code-.md)  
[传感器诊断工具](the-sensor-diagnostic-tool.md)  



