---
description: 测试和调试示例驱动程序
title: 测试和调试示例驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69831e8ffda3ac26e32bbac7694cbe56715bbeee
ms.sourcegitcommit: f8619f20a0903dd64f8641a5266ecad6df5f1d57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/29/2020
ms.locfileid: "91423514"
---
# <a name="testing-and-debugging-the-sample-driver"></a>测试和调试示例驱动程序

WDK 包含三个可用于测试和调试 WPD 驱动程序的工具。 下表描述了这些工具。

**工具**：说明

***WpdInfo.exe***：使用此工具，你可以打开或关闭设备、在设备上创建或删除对象、查看支持的命令、发出命令、查看事件、检索可读属性值以及设置可写属性值。

***WpdDeviceInspector.exe***：生成描述设备功能和内容的 HTML 报告。

***WpdMon.exe***：跟踪在 WPD 驱动程序和操作系统或 WPD 应用程序之间传递的消息和命令。

有关这些工具及其用法的详细信息，请参阅 WDK 文档中的 [WPD 驱动程序开发工具](familiarizing-yourself-with-the-sample-driver.md) 。

## <a name="tracking-the-sensor-reading-event-by-using-wpdinfoexe"></a>使用 WpdInfo.exe 跟踪传感器读取事件

在开始 *WpdInfo.exe*之前，请更新 WpdInfo 文件，其中包含将传感器读数的 PROPERTYKEYS \_ 和传感器 \_ 更新 \_ 间隔属性映射到相应友好字符串的条目。

```ManagedCPlusPlus
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.2, SENSOR_READING, VT_UI8
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.3, SENSOR_UPDATE_INTERVAL, VT_UI4
```

WpdInfo 文件在与 *WpdInfo.exe*相同的文件夹中。 如果此文件不存在，请运行 *WpdInfo.exe* 一次来生成该文件。

当你开始 *WpdInfo.exe*时，它会提示你从已安装 WPD 设备的列表中选择一个便携式设备。 选择传感器设备后，该工具会在其窗口的下窗格中记录事件。

![WpdInfo UI 下方窗格中的 TempHumidity 事件的日志](images/wpdinfo_temphumidity_object.png)

在上一示例中触发传感器读数事件时，以下信息为 true：

- 传感器读数传感器读数 \_ 为2170720417。 此值指示 2 (的传感器标识符，该标识符对应于 Sensiron 温度和湿度传感器) 、1个元素的计数、每个元素7个字节的大小、72.0 度的温度以及41.7% 的相对湿度。
- 其 interval 属性 "传感器 \_ 更新 \_ 间隔" 设置为2000。

## <a name="updating-the-interval-property-by-using-wpdinfoexe"></a>使用 WpdInfo.exe 更新 Interval 属性

选择视差 BS2 传感器设备后，可以使用该工具将间隔属性（传感器 \_ 更新 \_ 间隔）从其默认值 2000 ms 更改为其他值，介于2到60秒之间。

1. 第一个步骤要求从 "枚举" 窗格中选择 TempHumidity 函数对象，以显示该对象的所有属性值。 可以在最左侧的窗格中找到此对象作为设备对象的直接子对象。
2. 接下来，单击 " **传感器 \_ 更新 \_ 间隔**"，这将打开 " **编辑** " 对话框，你可以在其中将新值键入为 VT \_ UI4 类型。

!["wpd 信息" 工具在 "编辑" 对话框打开的情况下打开。](images/wpdinfo_interval.png)

允许的值范围介于02000和60000（含）之间。 单击 **"确定"**，新的 "间隔" 属性值将发送到设备。 观察事件窗格，可以在事件参数中看到带有新的更新间隔值的事件。

## <a name="debugging-the-driver-with-visual-studio-8"></a>用 Visual Studio 8 调试驱动程序

WPD 驱动程序基于 Windows 驱动程序框架 (WDF) UMDF 平台。 与内核模式驱动程序相比，UMDF 驱动程序提供更强的稳定性和安全性，以及性能可比较。 而且，UMDF 驱动程序允许使用用户模式调试器，如 Visual Studio 8。 在用户模式下调试驱动程序往往比在内核模式下调试更快，因为错误只影响当前进程而不影响整个计算机。

安装驱动程序后，可以通过执行以下步骤，在 Visual Studio 8 中创建调试项目：

1. 以提升的权限打开 Visual Studio 8 (以管理员身份运行) 并 &lt; &gt; 从现有代码路径导航到 "新建项目"。
    **注意**   必须以提升的权限打开 Visual Studio 8，因为 LocalService 帐户需要这些权限。 WUDFHost 进程在 LocalService 帐户中运行。 使用 Visual Studio 8 可以调试驱动程序项目。
2. 按照 **欢迎使用 "从现有代码文件创建项目" 向导**中的步骤进行操作。 请确保指定语言、驱动程序源文件的位置、项目名称，等等。
3. 打开新创建的项目。
4. 在 "**调试"/"附加到进程**" 菜单上的 "**附加到进程**" 对话框中显示的 "**可用进程**" 列表中，选择 " *WudfHost.exe* "。 如果有多个 *WudfHost.exe* 过程的实例，请选择已加载驱动程序 DLL 的实例。
5. 完成前面的步骤后，可以在源代码中设置断点并调试驱动程序。

## <a name="tips-for-debugging-wpd-driver-initialization-code"></a>调试 WPD 驱动程序初始化代码的技巧

WPD 驱动程序的初始化代码（例如，在打包到 WDK 的两个 WPD 示例驱动程序的 **WpdBaseDriver：： Initialize** 中找到的代码）在安装驱动程序以调试此初始化代码时运行，你应该使用 Windows 驱动程序工具包随附的 *您尚未 wdfverifier* 工具。 此工具使用户模式调试器可以在主机进程启动时自动启动，也可以在驱动程序加载时自动启动。

## <a name="related-topics"></a>相关主题

****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)
