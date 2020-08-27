---
description: 使用 WpdDeviceInspector 工具
title: 使用 WpdDeviceInspector 工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 827fbe8d7886662f114eece4134a9fcec5df9a2c
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969346"
---
# <a name="using-the-wpddeviceinspector-tool"></a>使用 WpdDeviceInspector 工具


WpdDeviceInspector 工具是一种控制台应用程序，用于生成综合性的 HTML 报告。 此报表介绍三个类别的设备和驱动程序信息，如下表中所列。

| 类别                 | 说明                                                                                              |
|--------------------------|----------------------------------------------------------------------------------------------------------|
| 安装信息 | 指定 Windows installer 使用的设备和驱动程序数据。                                  |
| 设备功能      | 标识设备支持的命令、对象、内容类型、格式和事件。       |
| 设备内容           | 列出对象标识符字符串和对应的持久唯一对象标识符 (PUID) 值。 |

 

## <a name="span-idviewing_the_command-line_options_for_wpddeviceinspectorspanspan-idviewing_the_command-line_options_for_wpddeviceinspectorspanspan-idviewing_the_command-line_options_for_wpddeviceinspectorspanviewing-the-command-line-options-for-wpddeviceinspector"></a><span id="Viewing_the_Command-Line_Options_for_WpdDeviceInspector"></span><span id="viewing_the_command-line_options_for_wpddeviceinspector"></span><span id="VIEWING_THE_COMMAND-LINE_OPTIONS_FOR_WPDDEVICEINSPECTOR"></span>查看 WpdDeviceInspector 的命令行选项


若要查看 *WpdDeviceInspector.exe*的命令行选项，请在命令提示符下键入以下命令：

```cmd
WpdDeviceInspector.exe /?
```

## <a name="span-idgenerating_a_report_for_a_specific_devicespanspan-idgenerating_a_report_for_a_specific_devicespanspan-idgenerating_a_report_for_a_specific_devicespangenerating-a-report-for-a-specific-device"></a><span id="Generating_a_Report_for_a_Specific_Device"></span><span id="generating_a_report_for_a_specific_device"></span><span id="GENERATING_A_REPORT_FOR_A_SPECIFIC_DEVICE"></span>为特定设备生成报告


通过运行不带任何参数的 *WpdDeviceInspector.exe* ，然后输入所选设备的索引，可以生成特定设备的报告。

```cpp
> WpdDeviceInspector.exe


1 Windows Portable Device(s) found on the system

[0]     Dev Interface: \\?\root#wpd#0001#{6ac27878-a6fa-4155-ba85-f98f491d4f33}
        Friendly Name: Hello World!
        Manufacturer:  Windows Portable Devices Group
        Description:   Hello World!

Enter the index of the device you want to Inspect.
>
```

或者，如果知道设备标识符，可以通过在命令提示符下直接在/Device 开关后面键入设备标识符，来告知*WpdDeviceInspector.exe* 始终为该设备生成报表：

```cmd
WpdDeviceInspector.exe /Device:\\?\root#wpd#0000#{6ac27878-a6fa-4155-ba85-f98f491d4f33}
```

启动*WpdDeviceInspector.exe*没有任何参数的情况下，设备标识符列在每个设备的*Dev 接口*条目下。

## <a name="span-idoperating_wpddeviceinspector_in_snapshot_modespanspan-idoperating_wpddeviceinspector_in_snapshot_modespanspan-idoperating_wpddeviceinspector_in_snapshot_modespanoperating-wpddeviceinspector-in-snapshot-mode"></a><span id="Operating_WpdDeviceInspector_in_Snapshot_Mode"></span><span id="operating_wpddeviceinspector_in_snapshot_mode"></span><span id="OPERATING_WPDDEVICEINSPECTOR_IN_SNAPSHOT_MODE"></span>在快照模式下运行 WpdDeviceInspector


你可以在快照模式下操作 *WpdDeviceInspector.exe* ，并捕获在给定设备上镜像对象层次结构的目录结构。 当该工具在快照模式下运行时，它将在存储给定对象的属性和属性的每个文件夹中创建 opt 文件。

在快照模式下，二进制资源将保存到为资源键命名的文件 () 。 可以根据需要重命名和打开这些文件。 例如，JPEG 图像的默认资源将保存到 {E81E79BE-34F0-41BF-B53F-F1A06AE87842}. 0，但可以轻松地重命名为设备 \_image.jpg，以便可以在图形工具中查看该图像。

若要在快照模式下操作，请在命令提示符下使用/Snapshot 开关：

```cmd
WpdDeviceInspector.exe /Snapshot
```

## <a name="span-idoperating_wpddeviceinspector_in_wpd_automation_modespanspan-idoperating_wpddeviceinspector_in_wpd_automation_modespanspan-idoperating_wpddeviceinspector_in_wpd_automation_modespanoperating-wpddeviceinspector-in-wpd-automation-mode"></a><span id="Operating_WpdDeviceInspector_in_WPD_Automation_Mode"></span><span id="operating_wpddeviceinspector_in_wpd_automation_mode"></span><span id="OPERATING_WPDDEVICEINSPECTOR_IN_WPD_AUTOMATION_MODE"></span>在 WPD 自动化模式下操作 WpdDeviceInspector


可以 *WpdDeviceInspector.exe* 来转储给定设备的 JScript 属性和方法。 当你使用 WPD 自动化从设备阶段™ HostedSiteWithDevice 任务访问 WPD 设备时，这非常有用。 有关为 WPD 设备创建设备阶段™任务的详细信息，请参阅 Windows 设备体验门户。 此功能仅适用于 Windows 7。

若要在 WPD Automation 模式下操作，请在命令提示符处使用/Automation 开关：

```cpp
WpdDeviceInspector.exe /Automation
```

 

 




