---
description: 在本主题中，你将使用随 Microsoft Visual Studio Professional 2019 一起提供的 USB 内核模式驱动程序模板来编写简单的内核模式驱动程序框架 (基于 KMDF) 的客户端驱动程序。
title: 如何编写第一个 USB 客户端驱动程序 (KMDF)
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 7d11dd381cede0b0ea123b356a1a11a9dda41562
ms.sourcegitcommit: d965aed20311ab46f05ca944c565053b5a22df2b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/30/2020
ms.locfileid: "91554221"
---
# <a name="how-to-write-your-first-usb-client-driver-kmdf"></a>如何编写第一个 USB 客户端驱动程序 (KMDF)


在本主题中，你将使用随 Microsoft Visual Studio Professional 2019 一起提供的 **USB 内核模式驱动程序** 模板来编写简单的内核模式驱动程序框架 (基于 KMDF) 的客户端驱动程序。 生成和安装客户端驱动程序后，你将在 **设备管理器** 中查看客户端驱动程序，并在调试器中查看驱动程序输出。

有关模板生成的源代码的说明，请参阅 [了解 USB 客户端驱动程序的 KMDF 模板代码](understanding-the-kmdf-template-code-for-usb.md)。

### <a name="prerequisites"></a>先决条件

若要开发、调试和安装内核模式驱动程序，需要两台计算机：

-   运行 Windows 7 或更高版本的 Windows 操作系统的主计算机。 主计算机是您的开发环境，您可以在其中编写和调试驱动程序。
-   运行 Windows Vista 或更高版本的 Windows 的目标计算机。 目标计算机具有要调试的内核模式驱动程序。

在开始之前，请确保满足以下要求：

**软件要求**

-   你的主计算机托管你的开发环境，并且具有 Visual Studio Professional 2019。
-   主计算机具有适用于 Windows 8 的最新 Windows 驱动程序工具包 (WDK) 。 工具包包括开发、生成和调试 KMDF 驱动程序所需的标头、库、工具、文档和调试工具。 若要获取最新版本的 WDK，请参阅 [下载 Windows 驱动程序工具包 (WDK) ](../download-the-wdk.md)。
-   您的主计算机具有适用于 Windows 的调试工具的最新版本。 可以从 WDK 获取最新版本，也可以 [下载和安装适用于 Windows 的调试工具](../download-the-wdk.md)。
-   你的目标计算机运行的是 Windows Vista 或更高版本的 Windows。
-   主机和目标计算机配置为进行内核调试。 有关详细信息，请参阅 [在 Visual Studio 中设置网络连接](../debugger/setting-up-a-network-debugging-connection-in-visual-studio.md)。

**硬件要求**

获取将为其写入客户端驱动程序的 USB 设备。 在大多数情况下，会向你提供 USB 设备及其硬件规范。 该规范描述了设备功能和支持的供应商命令。 使用规范来确定 USB 驱动程序的功能以及相关的设计决策。

如果你不熟悉 USB 驱动程序开发，请使用 OSR USB FX2 学习工具包来研究 WDK 附带的 USB 示例。 可以从 [OSR Online](https://www.osronline.com/)获取学习工具包。 它包含 USB FX2 设备以及实现客户端驱动程序所需的所有硬件规范。

还可以 (MUTT) 设备获取 Microsoft USB 测试工具。 可以从 [JJG 技术](http://www.jjgtechnologies.com/mutt.htm)购买 MUTT 硬件。 设备未安装安装的固件。 若要安装固件，请从 [该网站](./index.md) 下载 MUTT 软件包并运行 MUTTUtil.exe。 有关详细信息，请参阅包附带的文档。

**建议阅读**

-   [适用于所有驱动程序开发人员的概念](../gettingstarted/concepts-and-knowledge-for-all-driver-developers.md)
-   [设备节点和设备堆栈](../gettingstarted/device-nodes-and-device-stacks.md)
-   [Windows 驱动程序入门](../gettingstarted/index.md)
-   [内核模式驱动程序框架](../wdf/index.md)
-   *使用 Windows Driver Foundation 开发驱动程序*，由 "Orwick" 和 "专家 Smith" 编写。 有关详细信息，请参阅 [通过 WDF 开发驱动程序](../wdf/developing-drivers-with-wdf.md)。

<a name="instructions"></a>Instructions
------------

### <a name="step-1-generate-the-kmdf-driver-code-by-using-the-visual-studio-professional2019-usb-driver-template"></a><a href="" id="generate-the-kmdf-driver-code-by-using-the--visual-studio-professional-2019---usb-driver-template"></a>步骤1：使用 Visual Studio Professional 2019 USB 驱动程序模板生成 KMDF 驱动程序代码

有关生成 KMDF 驱动程序代码的说明，请参阅 [基于模板编写 KMDF 驱动程序](../gettingstarted/writing-a-kmdf-driver-based-on-a-template.md)中的步骤。

**对于 USB 特定的代码，请在 Visual Studio Professional 2019 中选择以下选项**

1.  在 " **新建项目** " 对话框顶部的 "搜索" 框中，键入 " **USB"。**
2.  在中间窗格中，选择 " **内核模式驱动程序"、"USB (KMDF) " **。
3.  选择“下一步”  。
4.  输入项目名称，选择 "保存位置"，然后选择 " **创建**"。

以下屏幕截图显示了**USB 内核模式驱动程序**模板的 "**新建项目**" 对话框。

![visual studio 新项目选项](images/kmdf-template-visual-studio-2019.png)

![visual studio 新项目选项第二屏幕](images/kmdf-template-visual-studio-2019-2.png)

本主题假定 Visual Studio 项目的名称为 "MyUSBDriver \_ "。 它包含以下文件：

| 文件                      | 说明                                                                                                          |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| 公有。h                   | 提供客户端驱动程序和与 USB 设备通信的用户应用程序共享的常见声明。 |
| * &lt; 项目名称 &gt; *.inf | 包含在目标计算机上安装客户端驱动程序所需的信息。                                   |
| Trace。h                    | 声明跟踪函数和宏。                                                                               |
| Driver .h;驱动程序。c         | 声明并定义驱动程序入口点和事件回调例程。                                                |
| 设备 .h;设备 c         | 声明并定义准备硬件事件的事件回调例程。                                          |
| Queue .h;Queue           | 声明并定义框架的队列对象所引发的事件的事件回调例程。                 |

 

### <a name="step-2-modify-the-inf-file-to-add-information-about-your-device"></a><a href="" id="modify-the-inf-file-to-add-information-about-your-device"></a>步骤2：修改 INF 文件以添加有关设备的信息

构建驱动程序之前，必须用有关设备的信息（尤其是硬件 ID 字符串）修改模板 INF 文件。

在 **解决方案资源管理器**的 " **驱动程序文件**" 下，双击 INF 文件。

在 INF 文件中，可以提供制造商和提供程序名称、设备安装程序类等信息。 您必须提供的一条信息是设备的硬件标识符。

若要提供硬件 ID 字符串：

1.  将 USB 设备连接到主机计算机，并让 Windows 枚举设备。
2.  打开 **设备管理器** 并打开设备的 "属性"。
3.  在 " **详细信息** " 选项卡上，选择 "属性" 下的 **Hardward id** **。**

    设备的硬件 ID 显示在列表框中。 选择并按住 (或右键单击) 并复制硬件 ID 字符串。

4.  \\ \_ 将以下行中的 USB VID VVVV&PID \_ pppp 替换为硬件 ID 字符串。

    `[Standard.NT$ARCH$] %MyUSBDriver_.DeviceDesc%=MyUSBDriver__Device, USB\VID_vvvv&PID_pppp`

### <a name="step-3-build-the-usb-client-driver-code"></a><a href="" id="build-the-usb-client-driver-code"></a>步骤3：生成 USB 客户端驱动程序代码

**构建驱动程序**

1.  在 Visual Studio Professional 2019 中打开驱动程序项目或解决方案
2.  选择并按住 (或右键单击) **解决方案资源管理器** 中的解决方案，然后选择 " **Configuration Manager**"。
3.  从 " **Configuration Manager**中，选择" **活动解决方案配置** " (例如， **Windows 8 调试** 或 **Windows 8 版本**) 和 **活动解决方案平台** (例如，Win32) 对应于你感兴趣的版本类型。
4.  在 " **生成** " 菜单中，选择 " **生成解决方案**"。

有关详细信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

### <a name="step-4-configure-a-computer-for-testing-and-debugging"></a><a href="" id="configure-a-computer-for-testing-and-debugging"></a>步骤4：配置计算机以进行测试和调试

若要测试和调试驱动程序，请在主计算机上运行调试器，并在目标计算机上运行该驱动程序。 到目前为止，你已在主计算机上使用 Visual Studio 来构建驱动程序。 接下来，需要配置目标计算机。 若要配置目标计算机，请按照 [设置计算机以进行驱动程序部署和测试](../gettingstarted/provision-a-target-computer-wdk-8-1.md)中的说明进行操作。

### <a name="step-5-enable-tracing-for-kernel-debugging"></a><a href="" id="enable-tracing-for-kernel-debugging"></a>步骤5：为内核调试启用跟踪

模板代码包含几个跟踪消息 (TraceEvents) ，可以帮助您跟踪函数调用。 源代码中的所有函数都包含标记例程的入口和出口的跟踪消息。 对于错误，跟踪消息包含错误代码和有意义的字符串。 由于已为驱动程序项目启用 WPP 跟踪，因此在生成过程中创建的 PDB 符号文件包含跟踪消息格式设置说明。 如果将主机和目标计算机配置为使用 WPP 跟踪，则驱动程序可以将跟踪消息发送到文件或调试器。

**为主机配置 WPP 跟踪**

1. 通过从 PDB 符号文件中提取跟踪消息格式设置说明， (TMF) 文件创建跟踪消息格式。

   您可以使用 Tracepdb.exe 来创建 TMF 文件。 该工具位于 WDK 的<em> &lt; install &gt; 文件夹</em>Windows 工具包 \\ 8.0 \\ bin \\ * &lt; 体系结构 &gt; *文件夹中。 以下命令将为驱动程序项目创建 TMF 文件。

   **tracepdb-f \[ PDBFiles \] -p \[ TMFDirectory\]**

   **-F**选项指定 PDB 符号文件的位置和名称。 **-P**选项指定由 Tracepdb 创建的 TMF 文件的位置。 有关详细信息，请参阅 [**Tracepdb 命令**](../devtest/tracepdb-commands.md)。

   在指定位置，将看到项目) 中每个 .c 文件 (一个文件。 它们具有 GUID 文件名。

2. 在调试器中，键入以下命令：
   1.  **。 load Wmitrace**

       加载 Wmitrace.dll 扩展。

   2.  **。链**

       验证是否已加载调试器扩展。

   3.  **！ wmitrace. searchpath + * * * &lt; TMF file location&gt;*

       将 TMF 文件的位置添加到调试器扩展的搜索路径。

       输出如下所示：

       `Trace Format search path is: 'C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE;c:\drivers\tmf'`

**将目标计算机配置为进行 WPP 跟踪**

1. 请确保目标计算机上已有 Tracelog 工具。 该工具位于 WDK 的 " <em> &lt; 安装 \_ " &gt; 文件夹</em>"Windows \\ \\ \\ * &lt; &gt; *工具包8.0 工具"。 有关详细信息，请参阅 [**Tracelog 命令语法**](../devtest/tracelog-command-syntax.md)。
2. 打开 **命令窗口** 并以管理员身份运行。
3. 键入以下命令：

   **tracelog-start MyTrace \# c918ee71-68c7-4140-8f7d-c907abbcb05d-旗 0xffff-level 7-**

   命令启动一个名为 MyTrace 的跟踪会话。

   **Guid**参数指定跟踪提供程序的 guid，它是客户端驱动程序。 可以从 Visual Studio Professional 2019 项目中的 Trace 获取 GUID。 作为另一种选择，可以键入以下命令，并在 guid.empty 文件中指定 GUID。 文件包含连字符格式的 GUID：

   **tracelog-start MyTrace-guid c： \\ 驱动 \\ 程序提供程序。 guid-标志 0xffff-级别 7-rt-kd**

   您可以通过键入以下命令来停止跟踪会话：

   **tracelog-停止 MyTrace**

### <a name="step-6-deploy-the-driver-on-the-target-computer"></a><a href="" id="deploy-the-driver-on-the-target-computer"></a>步骤6：在目标计算机上部署驱动程序

1. 在 "**解决方案资源管理器**" 窗口中，选择并按住 (或右键单击 " <em> &lt; 项目名称 &gt; </em>**包**") ，然后选择 "**属性**"。
2. 在左窗格中，导航到 " **配置属性 &gt; 驱动程序安装 &gt; 部署**"。
3. 选中 "启用部署"，并选中 "导入到驱动程序存储区"。
4. 对于 " **远程计算机名称**"，指定目标计算机的名称。
5. 选择“安装并验证”  。
6. 选择“确定”  。
7. 在“调试”  菜单上，选择“开始调试”  或按键盘上的 **F5**。

**注意**   请*不要*在**硬件 Id 驱动程序更新**下指定设备的硬件 id。 只有驱动程序的信息 (INF) 文件中，才能指定硬件 ID。

 

有关将驱动程序部署到 Visual Studio Professional 2019 的目标系统的详细信息，请参阅将 [驱动程序部署到测试计算机](/windows-hardware/drivers)。

你还可以使用设备管理器在目标计算机上手动安装驱动程序。 如果要从命令提示符安装驱动程序，可以使用以下实用程序：

-   [PnPUtil](../devtest/pnputil.md)

    此工具随 Windows 一起提供。 它在 Windows \\ System32 中。 您可以使用此实用工具将驱动程序添加到驱动程序存储区中。

    ```cmd
    C:\>pnputil /a m:\MyDriver_.inf
    Microsoft PnP Utility

    Processing inf : MyDriver_.inf
    Driver package added successfully.
    Published name : oem22.inf
    ```

    有关详细信息，请参阅 [PnPUtil 示例](../devtest/pnputil-examples.md)。

-   [**DevCon Update**](../devtest/devcon-update.md)

    此工具随 WDK 一起提供。 你可以使用它来安装和更新驱动程序。

    ```cmd
    devcon update c:\windows\inf\MyDriver_.inf USB\VID_0547&PID_1002\5&34B08D76&0&6
    ```

### <a name="step-7-view-the-driver-in-device-manager"></a><a href="" id="view-the-driver-in-device-manager"></a>步骤7：在设备管理器中查看驱动程序

1.  输入以下命令以打开 **设备管理器**：

    **devmgmt.msc**

2.  验证 **设备管理器** 显示以下节点的节点：

    **示例**

    **MyUSBDriver \_ 设备**

### <a name="step-8-view-the-output-in-the-debugger"></a><a href="" id="view-the-output-in-the-debugger"></a>步骤8：在调试器中查看输出

Visual Studio 首先在 " **输出** " 窗口中显示进度。 然后，将打开 **调试器**的 "即时" 窗口。 验证跟踪消息显示在主计算机上的调试器中。 输出应如下所示，其中 "MyUSBDriver \_ " 是驱动程序模块的名称：

```cpp
[3]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverContextCleanup Entry
[1]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverDeviceAdd Entry
[1]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]MyUSBDriver_EvtDriverDeviceAdd Exit
[0]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]DriverEntry Entry
[0]0004.0054::00/00/0000-00:00:00.000 [MyUSBDriver_]DriverEntry Exit
```

## <a name="related-topics"></a>相关主题
[了解 USB 客户端驱动程序的 KMDF 模板代码](understanding-the-kmdf-template-code-for-usb.md)  
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)