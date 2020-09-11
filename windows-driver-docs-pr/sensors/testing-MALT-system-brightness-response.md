---
title: 测试系统亮度响应
author: windows-driver-content
description: 本主题提供有关如何使用 MALT (Microsoft 环境光线工具) 作为轻测试解决方案的说明。
ms.assetid: f0ba2628-8752-467d-abf6-6447668ac244
ms.date: 12/13/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4c4d8e61d8f7274f4f9bc9fd93dd65c2445770e4
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009779"
---
# <a name="testing-system-brightness-response"></a>测试系统亮度响应

本主题提供有关如何使用 MALT (Microsoft 环境光线工具) 工具测试系统亮度响应的说明。

## <a name="test-requirements"></a>测试要求

1. **完全装配的 MALT。**   ["如何" 指南](testing-MALT-building-a-light-testing-tool.md)提供了有关如何生成 MALT 或使现有测试设备 MALT 兼容的说明。

2. **配备环境光线传感器的 Windows 设备。** MALT (或兼容) 旨在测试屏幕亮度。 要测试的系统 (SUT) 必须具有可调整的亮度。 [SensorExplorer](https://aka.ms/sensorexplorerblog) 可用于确定 Windows 识别的传感器。

## <a name="sensorexplorer"></a>SensorExplorer

使用 [SensorExplorer](https://aka.ms/sensorexplorerblog) 确认环境光线传感器是否存在。

![SensorExplorer](images/sensorexplorer.png)

1. **将 MALT 插入到 SUT 上的 USB 端口，并将 Arduino 程序上传到微控制器。** 适用于 MALT 的 Arduino 程序可在 [GitHub](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT) 上找到 (也可在 HLK) 中找到。 将其上传到微控制器。 可以打开**Arduino**  >  **工具**  >  **串行监视器**，并验证[微控制器命令](testing-MALT-auto-brightness.md)是否按预期方式工作。 然后，关闭串行监视器，使其无法保持 COM 端口繁忙。

2. **在 SUT 上安装 SensorExplorer。** 可从 [Microsoft 应用商店](https://aka.ms/sensorexplorer)下载 SensorExplorer。 
   
> [!Note] 
> 如果要进行手动亮度测试，请从 [GitHub](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT)下载 MALTUtil。 在 HLK 中也可以找到工具。
   
3. **为 SUT 配置 "背景色" 和 "睡眠"。**  配置脚本 [MALT_SUT_Setup.bat](https://github.com/Microsoft/busiotools/tree/master/sensors/Tools/MALT/Code/Scripts) 会正确设置设备进行测试。  在提升的命令提示符下运行 ``MALT_SUT_Setup.bat`` 并按照脚本说明进行操作。

## <a name="test-areas-to-consider"></a>要考虑的测试区域

下面是要考虑的其他测试区域的列表。

* 功能

    * [测试自动亮度](testing-MALT-auto-brightness.md)
    * [测试手动亮度](testing-MALT-manual-brightness.md)

* 施加

    * [测试系统方案](testing-MALT-system-scenarios.md)

## <a name="malt-sensor-placement"></a>MALT 传感器位置

![MALT 传感器位置](images/placement.png)

下面是有关 MALT 传感器布局的提示列表。

* 将 MALT 的屏幕传感器放到它所在的 SUT 屏幕上。
* MALT 环境传感器必须面对光源，并离开 SUT 的屏幕。 
* 请勿阻止 SUT 的 ALS 传感器。  板载传感器不得封闭像素 MALT 或任何其他障碍。
* 将灯具箱放置在 SUT 上，使光源口径朝上。 为了获得最佳效果，屏幕应平行于光源口径并面向光源口径。
* 不应将光线泄漏进机箱的底部。  仔细检查以确保传感器仍然存在。
* 在灯具机箱的内部或顶部装入光源。  如果光源装在灯具机箱顶部，则面板应放置在口径的顶部，使光源向下移动到机箱中。
* 不应从该框的顶部泄漏任何光线。 您根本看不到该框中的任何一种。


请参阅 [此白皮书](/windows-hardware/design/whitepapers/integrating-ambient-light-sensors-with-computers-running-windows-10-creators-update) ，了解有关如何集成光源传感器和环境光线响应曲线的 Microsoft 完整指导。