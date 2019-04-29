---
Description: 使用 WpdDeviceInspector 工具
title: 使用 WpdDeviceInspector 工具
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4aedc1f270b6995fb19b34d74e0b798763f7361b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370455"
---
# <a name="using-the-wpddeviceinspector-tool"></a>使用 WpdDeviceInspector 工具


WpdDeviceInspector 工具是一个控制台应用程序的全面的 HTML 报告。 此报告描述了下表中列出的三种类别的设备和驱动程序信息。

| Category                 | 描述                                                                                              |
|--------------------------|----------------------------------------------------------------------------------------------------------|
| 安装信息 | 指定由 Windows 安装程序使用的设备和驱动程序数据。                                  |
| 设备功能      | 标识命令、 对象、 内容类型、 格式和设备支持的事件。       |
| 设备内容           | 列出了对象标识符字符串和相应的永久唯一对象标识符 (PUID) 值。 |

 

## <a name="span-idviewingthecommand-lineoptionsforwpddeviceinspectorspanspan-idviewingthecommand-lineoptionsforwpddeviceinspectorspanspan-idviewingthecommand-lineoptionsforwpddeviceinspectorspanviewing-the-command-line-options-for-wpddeviceinspector"></a><span id="Viewing_the_Command-Line_Options_for_WpdDeviceInspector"></span><span id="viewing_the_command-line_options_for_wpddeviceinspector"></span><span id="VIEWING_THE_COMMAND-LINE_OPTIONS_FOR_WPDDEVICEINSPECTOR"></span>查看 WpdDeviceInspector 的命令行选项


若要查看的命令行选项*WpdDeviceInspector.exe*，在命令提示符下键入以下命令：

```cmd
WpdDeviceInspector.exe /?
```

## <a name="span-idgeneratingareportforaspecificdevicespanspan-idgeneratingareportforaspecificdevicespanspan-idgeneratingareportforaspecificdevicespangenerating-a-report-for-a-specific-device"></a><span id="Generating_a_Report_for_a_Specific_Device"></span><span id="generating_a_report_for_a_specific_device"></span><span id="GENERATING_A_REPORT_FOR_A_SPECIFIC_DEVICE"></span>为特定设备生成的报表


可以通过运行生成的特定设备的报告*WpdDeviceInspector.exe*而无需任何参数，并输入所选设备的索引。

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

或者，如果您知道设备标识符，您可以告诉*WpdDeviceInspector.exe*始终通过直接在命令提示符下 /Device 切换后键入设备标识符来生成用于该设备的报表：

```cmd
WpdDeviceInspector.exe /Device:\\?\root#wpd#0000#{6ac27878-a6fa-4155-ba85-f98f491d4f33}
```

下面列出的设备标识符*开发人员接口*则在启动时每个设备条目*WpdDeviceInspector.exe*不带任何参数。

## <a name="span-idoperatingwpddeviceinspectorinsnapshotmodespanspan-idoperatingwpddeviceinspectorinsnapshotmodespanspan-idoperatingwpddeviceinspectorinsnapshotmodespanoperating-wpddeviceinspector-in-snapshot-mode"></a><span id="Operating_WpdDeviceInspector_in_Snapshot_Mode"></span><span id="operating_wpddeviceinspector_in_snapshot_mode"></span><span id="OPERATING_WPDDEVICEINSPECTOR_IN_SNAPSHOT_MODE"></span>在快照模式下运行 WpdDeviceInspector


你可以经营*WpdDeviceInspector.exe*在快照模式下和捕获镜像对象层次结构中的给定设备上的目录结构。 当在快照模式下运行该工具时，它存储给定的对象的属性和属性的每个文件夹中创建.opt 文件。

在快照模式下的二进制资源将保存到命名的资源键 (GUID.pid) 的文件。 可以重命名并根据需要打开这些文件。 例如，将 JPEG 图像的默认资源保存到 {E81E79BE-34F0-41BF-B53F-F1A06AE87842}.0，但无法轻松地重命名为设备\_image.jpg 以便可以在图形工具中查看该映像。

在快照模式下操作，请在命令提示符下使用 /Snapshot 开关：

```cmd
WpdDeviceInspector.exe /Snapshot
```

## <a name="span-idoperatingwpddeviceinspectorinwpdautomationmodespanspan-idoperatingwpddeviceinspectorinwpdautomationmodespanspan-idoperatingwpddeviceinspectorinwpdautomationmodespanoperating-wpddeviceinspector-in-wpd-automation-mode"></a><span id="Operating_WpdDeviceInspector_in_WPD_Automation_Mode"></span><span id="operating_wpddeviceinspector_in_wpd_automation_mode"></span><span id="OPERATING_WPDDEVICEINSPECTOR_IN_WPD_AUTOMATION_MODE"></span>在 WPD 自动化模式下运行 WpdDeviceInspector


你可以经营*WpdDeviceInspector.exe*要转储的 JScript 属性和方法的给定设备。 使用 WPD 自动化从 Device Stage™ HostedSiteWithDevice 任务访问 WPD 设备时，这是非常有用。 有关创作的 WPD 设备 Device Stage™ 任务的详细信息，请参阅 Windows 设备体验门户。 此功能才可用在 Windows 7 中。

若要在 WPD 自动化模式下操作，请在命令提示符下使用 /Automation 开关：

```cpp
WpdDeviceInspector.exe /Automation
```

 

 




