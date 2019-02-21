---
title: 测试系统亮度响应
author: windows-driver-content
description: 本主题提供有关如何使用 MALT （Microsoft 环境光工具） 的说明作为测试解决方案的光。
ms.assetid: f0ba2628-8752-467d-abf6-6447668ac244
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9980569f59ce92741a5cfab9db3bf5bb5b84e3ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541449"
---
# <a name="testing-system-brightness-response"></a>测试系统亮度响应

本主题将说明了如何通过使用 MALT （Microsoft 环境光工具） 工具测试系统亮度响应。

## <a name="test-requirements"></a>测试要求

1. **完全装配 MALT。**   ["如何"指南](testing-MALT-building-a-light-testing-tool.md)说明了如何生成 MALT 或使现有测试探测 MALT 设备兼容。

2. **配备有一个环境光线传感器的 Windows 设备。** MALT （或兼容） 被旨在测试屏幕亮度。 待测系统 (SUT) 必须具有可调整亮度。 [SensorExplorer](https://aka.ms/sensorexplorerblog)可用于确定被 Windows 识别的传感器。

## <a name="sensorexplorer"></a>SensorExplorer

使用[SensorExplorer](https://aka.ms/sensorexplorerblog)确认环境光线传感器是否存在。

![SensorExplorer](images/sensorexplorer.png)

1. **MALT 插入 SUT 上的 USB 端口，并将 arduino 开发程序上传到微型控制器。** MALT arduino 开发程序，可[GitHub](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT) （也在 HLK)。 将其上载到微型控制器。 您可以打开**Arduino** > **工具** > **串行监视器**，并确认[微控制器命令](testing-MALT-auto-brightness.md)按预期方式工作。 然后，关闭串行监视器，以便它不会保留 COM 端口正忙。

2. **SUT 上安装 SensorExplorer。** 可以从下载 SensorExplorer [Microsoft 应用商店](https://aka.ms/sensorexplorer)。 
   
> [!Note] 
> 如果你想要执行手动亮度测试，下载从 MALTUtil [GitHub](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT)。 工具还可在 HLK。
   
3. **配置背景色和 SUT 的睡眠状态。**  配置脚本[MALT_SUT_Setup.bat](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Code/Scripts)将正确安装程序用于测试你的设备。  在提升的命令提示符处运行``MALT_SUT_Setup.bat``按照脚本说明进行操作。

## <a name="test-areas-to-consider"></a>测试需要考虑的方面

下面是需要考虑的其他测试方面的列表。

* 功能

    * [测试自动亮度](testing-MALT-auto-brightness.md)
    * [测试手动亮度](testing-MALT-manual-brightness.md)

* 压力

    * [测试系统方案](testing-MALT-system-scenarios.md)

## <a name="malt-sensor-placement"></a>MALT 传感器放置

![MALT 传感器放置](images/placement.png)

下面是有关 MALT 传感器位置的提示的列表。

* 将放置到 SUT 的屏幕，它朝上 MALT 屏幕传感器。
* MALT 环境传感器必须面对针对光源和离开 SUT 的屏幕。 
* 不会阻止 SUT 的 ALS 传感器。  板载传感器必须不是封闭的像素由 MALT 或任何其他障碍物。
* 将浅机箱放置上方 SUT，以便向上面向浅 aperture。 为获得最佳结果，应并行浅 aperture 和面向浅 aperture 屏幕。
* 应在泄漏无光，传入或传出的机箱底部。  仔细检查以确保传感器仍位于适当位置。
* 装载光源内部或浅色机箱之上。  如果基础浅机箱上装入的光源，则在面板应置于之上 aperture 上的框，光很抢眼是关闭入机箱。
* 应在没有 light 泄漏顶部的框。 不应能够看到所有框内。


请参阅[本白皮书](https://docs.microsoft.com/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update)有关 Microsoft 的完整指导集成光线传感器和环境光线响应曲线。