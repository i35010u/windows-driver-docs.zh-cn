---
title: 用 SensorExplorer 进行测试
description: 使用 SensorExplorer 进行传感器测试和日志记录
ms.date: 02/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: f0b7974a361853e07ed6d4384bc67f74dcba34ed
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719510"
---
# <a name="sensorexplorer-overview"></a>SensorExplorer 概述

SensorExplorer 是 [Microsoft Store](https://www.microsoft.com/p/sensorexplorer/9pgl3xpq1tpx?activetab=pivot:overviewtab) 上可用的应用程序，可通过 [GitHub](https://github.com/microsoft/busiotools/tree/master/sensors/Tools/SensorExplorer)访问应用程序包。 SensorExplorer 提供测试以快速验证支持的传感器的安装，如 (加速感应程序、简单方向传感器等的方向传感器 ) 并提供支持监视不同传感器的详细表格和绘图。 SensorExplorer 还提供可供调试的日志记录。

可以通过 SensorExplorer 左侧的菜单栏使用三种模式：

![SensorExplorer 概述](images/sensor-explorer-overview.png)

- **测试：** 用于手动测试支持的传感器。 方向测试将验证方向传感器是否安装在正确的位置，以及传感器数据是否与预期相同。 其他测试（如频率、偏移量和抖动）也可用。 使用 [UWP 传感器 API](/uwp/api/Windows.Devices.Sensors)读取传感器数据。

- **查看：** 用于查看传感器数据和属性。 在此模式下，应用显示了来自各种传感器（如加速感应器、罗盘、陀螺测试仪、倾斜仪、光传感器和方向传感器）的数据可视化，并以表格格式显示详细的传感器信息。 这可监视传感器的任何异常行为，还可以用于设置传感器的报告间隔。

- **MALT：** 用于连接和控制 [MALT (Microsoft 环境轻型工具)](./testing-malt-building-a-light-testing-tool.md)，这是一个简单的低成本轻型测试设备。 该工具结合了微控制器、光传感器和一个可控制的光源面板来校准光源传感器，并以可视方式测量面板的光线曲线。

## <a name="how-to-test-your-sensors-with-sensorexplorer"></a>如何通过 SensorExplorer 测试传感器

可以通过滚动顶部菜单栏来浏览可用于每个传感器的测试，屏幕快照中突出显示的屏幕显示为红色框。

![SensorExplorer 测试](images/sensor-explorer-tests.png)

### <a name="sensorexplorer-orientation-test"></a>SensorExplorer 方向测试

此测试要求你按不同方向定向设备，然后相应地检查传感器读数。 在测试结束时，将显示通过/失败结果。

#### <a name="before-beginning-orientation-tests"></a>开始方向测试之前

在测试模式下，如果在设备旋转后显示 "旋转"，则在 "设置" 中关闭自动旋转 (搜索 "旋转锁定"，并将其启用) 。 否则，不需要关闭自动旋转。 有关方向和参考框架的详细信息，请参阅 [设备参考框架部分](/windows-hardware/design/whitepapers/integrating-motion-and-orientation-sensors)。

#### <a name="starting-the-tests"></a>启动测试

单击 "启动" 按钮以开始测试。 对于每个测试，你都有10秒钟的时间来定向设备，以便屏幕上的箭头向下指。

注意：

- 您可以单击下面屏幕截图中突出显示的图标 (为红色框) 在测试过程中隐藏菜单栏。

- 菜单栏在测试期间处于禁用状态，并且在测试完成后才会启用。

- 对于简单方向传感器，测试的四个方向正面朝下、朝下、向左和向右。 对于所有其他传感器，四个测试方向为向上、向下、向左和向右。

![SensorExplorer 方向](images/sensor-explorer-orientation.png)

当传感器数据反映设备确实处于所需方向时，将显示绿色的复选标记。 你将自动转到下一个测试。

![SensorExplorer 方向成功](images/sensor-explorer-orientation-success.png)

否则，10秒后会显示红色 x，因为这一轮测试已失败。

![SensorExplorer 定向失败](images/sensor-explorer-orientation-fail.png)

#### <a name="after-the-tests"></a>测试后

单击 "保存日志" 按钮保存日志文件， (所有测试轮的数据将保存) ，或者单击 "重新启动" 按钮开始另一个测试。

### <a name="frequency-test"></a>频率测试

计算接收的传感器读数数/60 秒。 将在测试结束时显示数值。

### <a name="offset-test"></a>偏移测试

计算传感器读数与预期值进行比较时的平均误差。 将在测试结束时显示数值。

### <a name="jitter-test"></a>抖动测试

计算一段时间内传感器读数的最大差值，与初始读数比较。 将在测试结束时显示数值。

## <a name="how-to-monitor-your-sensors"></a>如何监视传感器

**视图** 模式自动检测附加到平台或嵌入到平台中的任何传感器，并显示从传感器读取的信息。 滚动菜单栏顶部 (在屏幕截图中突出显示的菜单栏中显示为红色框，) 更改正在显示的传感器。 对于每个传感器，当前数据和属性都显示在一个表中，并绘制为移动波形。 可在此处更改特定传感器的报告间隔。

![SensorExplorer 表](images/sensor-explorer-table.png)

## <a name="additional-information-on-logging"></a>有关日志记录的其他信息

"保存日志" 按钮将提示输入 ETL (事件跟踪日志) 文件的名称和位置，其默认名称为 "SensorExplorerLog"。 若要查看 ETL 文件，请使用 [tracerpt 命令](/windows-server/administration/windows-commands/tracerpt_1)。

![SensorExplorer 日志](images/sensor-explorer-log.png)

将记录以下内容：

- 所选传感器的属性
- 有关每个测试的信息
- 对于方向测试：
  - 通过测试时的传感器读数
  - 在倒计时结束之前的最后一个传感器读数，在这种情况下，测试未通过
- 对于其他测试：
  - 测试过程中收集的所有传感器读数
  - 最终结果