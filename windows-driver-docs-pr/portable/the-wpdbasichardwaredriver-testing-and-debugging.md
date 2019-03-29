---
Description: Testing and Debugging the Sample Driver
title: 测试和调试示例驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f54469f5c79fb6c1967aa016a1f2c6faac5add13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564408"
---
# <a name="testing-and-debugging-the-sample-driver"></a>测试和调试示例驱动程序


WDK 包括三个工具，可用于测试和调试 WPD 驱动程序。 这些工具是下表中所述。

|                          |                                                                                                                                                                                                                  |
|--------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 工具                     | 描述                                                                                                                                                                                                      |
| *WpdInfo.exe*            | 利用此工具可以打开或关闭设备、 创建或删除设备，查看受支持的命令，发出命令的对象，查看事件，检索可读属性值，并设置可写属性值。 |
| *WpdDeviceInspector.exe* | 生成 HTML 报表，其中介绍了设备功能和内容。                                                                                                                                     |
| *WpdMon.exe*             | 跟踪消息和 WPD 驱动程序和操作系统或 WPD 应用程序之间传递的命令。                                                                                                 |

 

有关这些工具及其用法的详细信息，请参阅[WPD 驱动程序开发工具](familiarizing-yourself-with-the-sample-driver.md)WDK 文档中。

## <a name="span-idtrackingthesensorreadingeventbyusingwpdinfoexespanspan-idtrackingthesensorreadingeventbyusingwpdinfoexespantracking-the-sensor-reading-event-by-using-wpdinfoexe"></a><span id="tracking_the_sensor_reading_event_by_using_wpdinfo.exe"></span><span id="TRACKING_THE_SENSOR_READING_EVENT_BY_USING_WPDINFO.EXE"></span>通过使用 WpdInfo.exe 跟踪传感器读取事件


在开始之前*WpdInfo.exe*，使用传感器映射 PROPERTYKEYs 条目更新 WpdInfo.Properties 文件\_读取和传感器\_更新\_间隔的属性相应的友好字符串。

```ManagedCPlusPlus
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.2, SENSOR_READING, VT_UI8
{a7ef4367-6550-4055-b66f-be6fdacf4e9f}.3, SENSOR_UPDATE_INTERVAL, VT_UI4
```

与位于同一文件夹中找到 WpdInfo.Properties 文件*WpdInfo.exe*。 如果此文件不存在，运行*WpdInfo.exe*一次，以生成它。

当您启动*WpdInfo.exe*，它会提示你从已安装 WPD 设备的列表中选择便携式设备。 选择该传感器设备后，该工具在其窗口的下部窗格中记录事件。

![wpd 信息工具](images/wpdinfo_temphumidity_object.png)

传感器读数事件触发在前面的示例，以下信息的一点是：

-   传感器读数属性，传感器\_阅读，已 2170720417。 此值指示的传感器标识符为 2 （这对应于 Sensiron 温度和湿度传感器），1 个元素，包括每个元素的 7 字节的大小，72.0 华氏度温度的计数和相对湿度的 41.7%。
-   其时间间隔属性，传感器\_更新\_间隔设置为 2,000。

## <a name="span-idupdatingtheintervalpropertybyusingwpdinfoexespanspan-idupdatingtheintervalpropertybyusingwpdinfoexespanupdating-the-interval-property-by-using-wpdinfoexe"></a><span id="updating_the_interval_property_by_using_wpdinfo.exe"></span><span id="UPDATING_THE_INTERVAL_PROPERTY_BY_USING_WPDINFO.EXE"></span>使用 WpdInfo.exe 更新间隔属性


选择视差 BS2 传感器设备后，可以使用该工具来更改间隔属性，传感器\_更新\_间隔，其默认值为 2,000 毫秒到另一个值，介于 2 到 60 秒之间。

1.  第一步需要可从枚举窗格中显示所有属性选择 TempHumidity 功能对象，该对象值。 您可以找到此对象为最左侧的窗格上的设备对象的直接子级。
2.  接下来，单击**传感器\_更新\_间隔**，这将打开**编辑**对话框中，可在其中键入新值为 VT\_UI4 类型。

![wpd 信息工具](images/wpdinfo_interval.png)

允许的值范围为 02000 到 60000，非独占。 单击**确定**，并向设备发送新的间隔属性值。 观察事件窗格中，并可以查看到达新的更新间隔值与在事件参数的事件。

## <a name="span-iddebuggingthedriverwithvisualstudio8spanspan-iddebuggingthedriverwithvisualstudio8spanspan-iddebuggingthedriverwithvisualstudio8spandebugging-the-driver-with-visual-studio-8"></a><span id="Debugging_the_Driver_with_Visual_Studio_8"></span><span id="debugging_the_driver_with_visual_studio_8"></span><span id="DEBUGGING_THE_DRIVER_WITH_VISUAL_STUDIO_8"></span>调试使用 Visual Studio 8 驱动程序


WPD 驱动程序基于 Windows 驱动程序框架 (WDF) UMDF 平台。 UMDF 驱动程序提供更大的稳定性和安全性，以及可比较的性能，比内核模式驱动程序。 和 UMDF 驱动程序允许用户模式调试程序，如 Visual Studio 8 中使用。 调试在用户模式下的驱动程序往往是比因为错误会影响整个计算机而不只是当前进程在内核模式下调试更快。

您的驱动程序安装后，可以在 Visual Studio 8 创建调试项目，通过执行以下步骤：

1.  使用提升的权限 （以管理员身份运行） 打开 Visual Studio 8 并导航到的文件&lt;新建&gt;从现有代码路径的项目。
    **请注意**  因为 LocalService 帐户需要这些权限，必须使用提升的权限打开 Visual Studio 8。 WUDFHost 进程运行 LocalService 帐户中。 通过使用 Visual Studio 8，您将能够调试驱动程序项目。

     

2.  按照中的步骤**欢迎使用从现有代码文件向导创建项目**。 请确保指定的语言的驱动程序源文件，项目名称、 位置等等。
3.  打开新创建的项目。
4.  上**调试/附加到进程**菜单中，选择*WudfHost.exe*中**可用进程**列表中显示的**附加到进程**对话框。 如果有多个实例的*WudfHost.exe*处理时，选择已加载的驱动程序的 DLL。
5.  完成前面的步骤后，可以在源代码中设置断点和调试您的驱动程序。

## <a name="span-idtipsfordebuggingwpddriverinitializationcodespanspan-idtipsfordebuggingwpddriverinitializationcodespanspan-idtipsfordebuggingwpddriverinitializationcodespantips-for-debugging-wpd-driver-initialization-code"></a><span id="Tips_for_Debugging_WPD_Driver_Initialization_Code"></span><span id="tips_for_debugging_wpd_driver_initialization_code"></span><span id="TIPS_FOR_DEBUGGING_WPD_DRIVER_INITIALIZATION_CODE"></span>调试 WPD 驱动程序初始化代码的提示


初始化代码将 WPD 驱动程序，例如，代码中找到**WpdBaseDriver::Initialize**在两个 WPD 示例驱动程序与 WDK 打包在一起，在运行时您的驱动程序安装调试此初始化代码，您应使用*WDFVerifier*是 Windows 驱动程序工具包附带的工具。 此工具，用户模式的调试程序在主机进程启动时，或在驱动程序加载时自动启动。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


****
[WpdBasicHardwareDriverSample](the-wpdbasichardwaredriver-sample.md)

[WPD 驱动程序示例](the-wpd-driver-samples.md)

 

 





