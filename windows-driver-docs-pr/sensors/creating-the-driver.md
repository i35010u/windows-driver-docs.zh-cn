---
title: 创建传感器驱动程序
description: 创建传感器驱动程序
ms.assetid: 7a1cea3c-d542-47e9-90f9-18bae4969b9f
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8da141f0a9ccd5603212cb8c2b81ef648910e510
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837624"
---
# <a name="creating-a-sensor-driver"></a>创建传感器驱动程序


如果你的传感器使用 HID，则建议你使用收件箱 HID 类驱动程序，而不是创建驱动程序。 如果传感器使用的传输不是 HID，则应该从[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)或 SpbAccelerometer 示例开始。

这些示例为传感器驱动程序所需的类和 COM 接口提供基本的工作实现。 以下过程显示了从示例创建驱动程序时应遵循的步骤：

1.  按照[创建永久唯一标识符](creating-a-persistent-unique-identifier.md)主题中提供的说明进行操作，以确保你的驱动程序是唯一的。 使用示例驱动程序源时，应始终提供新的**GUID**和其他标识符。

2.  添加一个类，用于处理与设备硬件的通信，如果你的传感器是逻辑传感器，则使用软件数据提供程序。

3.  根据需要添加对事件的支持。 您必须编写代码以创建一个线程，以便在特定的时间间隔引发事件。 还必须更新 SensorDdi 中的[**ISensorDriver：： OnGetSupportedEvents**](https://docs.microsoft.com/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensordriver-ongetsupportedevents)的实现，以报告驱动程序可以引发的事件列表。

4.  删除不需要的任何代码。

## <a name="build-the-driver"></a>构建驱动程序

若要构建你的驱动程序，请执行以下步骤：

1.  开始 Microsoft Visual Studio 2012。
2.  选择生成配置（例如，"调试"）和体系结构（例如，Win32）。
3.  打开驱动程序的解决方案或项目文件。
4.  选择 "生成/生成解决方案"。

## <a name="install-the-sensors-geolocation-driver-sample-for-testing"></a>安装传感器地理位置驱动程序示例以进行测试

若要安装用于测试的驱动程序，请执行以下步骤：

1.  请确保你的驱动程序生成时没有错误。

2.  将驱动程序的 DLL 和 INF 文件复制到一个单独的文件夹中。

3.  从你安装了 WDK 的 " *\_类型*" 文件夹中找到两个共同安装程序 DLL 文件（选中或免费）。 将这些文件复制到你在步骤3中创建的文件夹。 例如，如果在驱动器 C 上安装了 WDK，则可以将 WUDFUpdate\_01009 从 C：\\WinDDK\\*生成\#* \\\\\\

4.  运行 Devcon。 可以在安装 WDK 的工具\\devcon 文件夹中找到此程序。 例如，对于名为 WDKExample 的传感器，你可以键入：

    **devcon setup.exe install WDKExample "传感器\\WDKExample"**

    **请注意**  请勿使用 Devcon 安装已发布的驱动程序。 此建议仅用于测试。

     

如果无法安装您的驱动程序，则步骤2中的其中一种方法可能会返回错误代码。 若要调试此问题，必须在安装过程中附加一个调试器。 有关如何在加载过程中调试 UMDF 驱动程序的信息，请参阅[确定启动 Umdf 驱动程序失败的原因或启动 Umdf 设备失败](https://docs.microsoft.com/windows-hardware/drivers/wdf/determining-why-the-umdf-driver-fails-to-load-or-the-umdf-device-fails)。

还应验证你在 INF 文件中提供的类 ID 是否与用于驱动程序组件类的 IDL 文件中使用的**GUID**匹配。

## <a name="uninstalling-the-driver"></a>卸载驱动程序

可能需要在测试过程中卸载该驱动程序，例如，当你想要在更改代码后更新驱动程序安装时。 若要卸载该驱动程序，请执行以下步骤：

1.  打开**设备管理器**。 例如，单击 "**开始**"，然后在 "**开始搜索**" 框中键入以下。

    ``` syntax
    Device Manager
    ```

    之后，按 CTRL + ENTER。

2.  展开 "传感器" 节点。

3.  右键单击您的驱动程序的名称，然后单击 "**卸载**"。

4.  选择 **"删除此设备的驱动程序软件"** 。

5.  单击“确定”。

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://docs.microsoft.com/windows-hardware/drivers/gnss/sensors-geolocation-driver-sample)



