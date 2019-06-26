---
title: 创建传感器驱动程序
description: 创建传感器驱动程序
ms.assetid: 7a1cea3c-d542-47e9-90f9-18bae4969b9f
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 138949e47b4b517d9aa1028a0f55649c704d5e74
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67360689"
---
# <a name="creating-a-sensor-driver"></a>创建传感器驱动程序


如果您的传感器使用 HID 建议，而不是创建一个驱动程序，则使用收件箱 HID 类驱动程序。 如果您的传感器使用 HID 以外的传输，应该是以开始[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)或 SpbAccelerometer 示例。

这些示例提供的类和所需的传感器驱动程序的 COM 接口的基本工作实现。 以下过程显示了应遵循从示例创建一个驱动程序的步骤：

1.  按照中提供的说明操作[创建持久的唯一标识符](creating-a-persistent-unique-identifier.md)主题，请确保您的驱动程序是唯一的。 当使用示例驱动程序源时，始终提供新**GUID**s 和其他标识符。

2.  添加一个类来处理与你的设备硬件或软件的数据提供程序的通信，如果您的传感器是逻辑传感器。

3.  根据需要添加对事件的支持。 您必须编写代码以创建一个线程以在特定时间间隔引发事件。 您还必须更新的实现[ **ISensorDriver::OnGetSupportedEvents** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents) SensorDdi.cpp 报告的驱动程序可以引发的事件列表中。

4.  删除不需要任何代码。

## <a name="build-the-driver"></a>生成该驱动程序

若要生成您的驱动程序，请执行以下步骤：

1.  启动 Microsoft Visual Studio 2012。
2.  选择生成配置 （例如，调试） 和 （例如 Win32） 的体系结构。
3.  打开您的驱动程序的解决方案或项目文件。
4.  选择内部版本/内部版本的解决方案。

## <a name="install-the-sensors-geolocation-driver-sample-for-testing"></a>安装用于测试的传感器地理位置驱动程序示例

若要安装驱动程序进行测试，请执行以下步骤：

1.  请确保您的驱动程序生成且未出错。

2.  将您的驱动程序的 DLL 和 INF 文件复制到单独的文件夹。

3.  查找两个辅助安装程序 DLL 文件 （已检查或免费） 从 redist/wdf/*处理器\_类型*安装 WDK 文件夹。 将这些文件复制到步骤 3 中创建的文件夹。 例如，如果您安装 WDK 驱动器 C 上，您可以复制 WUDFUpdate\_从 c: 01009.dll\\WinDDK\\*生成\#* \\redist\\wdf\\x86。

4.  运行 Devcon.exe。 可以在工具中找到此程序\\安装 WDK devcon 文件夹。 例如，对于名为 WDKExample 传感器，则键入：

    **devcon.exe 安装 WDKExample.inf"传感器\\WDKExample"**

    **请注意**  不使用 Devcon.exe 安装已发布的驱动程序。 此建议是仅用于测试。

     

如果不能安装您的驱动程序，它可能是在步骤 2 返回了错误代码中的方法之一。 若要调试此问题，你必须在安装过程中附加调试器。 有关如何在加载期间调试 UMDF 驱动程序的信息，请参阅[确定为何 UMDF 驱动程序无法加载或 UMDF 设备故障到开始](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)。

您还应该验证提供在 INF 文件匹配的类 ID，您**GUID**驱动程序的 IDL 文件中使用的组件类。

## <a name="uninstalling-the-driver"></a>卸载该驱动程序

您可能需要卸载该驱动程序在测试期间，例如当你想要对代码进行更改后更新驱动程序安装。 若要卸载该驱动程序，请按照下列步骤：

1.  打开**设备管理器**。 例如，单击**启动**，然后在**开始搜索**框中，键入以下内容。

    ``` syntax
    Device Manager
    ```

    之后，按 CTRL + ENTER。

2.  展开传感器节点。

3.  右键单击您的驱动程序的名称，然后单击**卸载**。

4.  选择**删除此设备的驱动程序软件**。

5.  单击 **“确定”** 。

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



