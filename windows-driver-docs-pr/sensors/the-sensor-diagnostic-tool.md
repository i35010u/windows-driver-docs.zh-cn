---
title: 使用传感器诊断工具测试传感器功能
description: 使用传感器诊断工具来测试您的驱动程序、 固件和硬件的功能。
ms.assetid: 447E1348-53BA-4AD4-9010-A6452F46A827
keywords:
- 测试传感器
- 传感器测试
- 传感器诊断工具
- 传感器驱动程序测试
- 传感器固件测试
- 传感器硬件测试
- 传感器事件
- 传感器，报表时间间隔内
- 传感器，变化敏感度
- 报告间隔
- 更改敏感度
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9436c96016c702efdc95c1fe32919b7d6b4b6dce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575244"
---
# <a name="testing-sensor-functionality-with-the-sensor-diagnostic-tool"></a>使用传感器诊断工具测试传感器功能


使用传感器诊断工具来测试您的驱动程序、 固件和硬件的功能。

若要测试的传感器和位置 API，将调用该工具：

-   数据检索
-   事件处理
-   报告间隔
-   更改敏感度
-   属性检索

而不是编写的应用程序来执行这些测试，可以使用传感器诊断工具，它作为 Windows 驱动程序工具包 (WDK) 的一部分提供。

例如，如果驱动程序开发计算机是基于 x64 的计算机，并在默认位置安装了 WDK，那么您将找到传感器诊断工具在以下文件夹中：

*C:\\Program Files (x86)\\Windows 工具包\\10\\工具\\x64\\sensordiagnostictool.exe*后安装传感器或位置驱动程序和硬件附加到您的 PC，该工具会立即识别并在可用传感器的列表中记录你的设备。

多个传感器连接到 PC 时，下图显示了传感器诊断工具启动屏幕。 在 PC 上可用传感器的左窗格中显示。

![传感器诊断工具： 启动](images/sdt-startup.png)

在这种情况下，传感器诊断工具检测到的 HID 传感器，以及简单的设备方向传感器、 Windows 位置提供程序和地理位置传感器支持地理位置驱动程序示例的集合存在。

## <a name="support-for-ambient-light-sensors"></a>对环境光线传感器的支持


传感器诊断工具包括对环境光线传感器 (ALS) 支持。 在 SB %框中，该工具的左上角报告当前显示亮度。

但是，务必请注意，当该工具检索 ALS 值时，它会返回这些值作为 （LUX，偏移量） 对。 此排序不同于高级配置和电源接口 (ACPI) 标准的 （偏移量，LUX） 对。

## <a name="related-topics"></a>相关主题
[测试传感器功能](testing-sensor-functionality.md)  
[测试位置的功能](testing-location-functionality.md)  



