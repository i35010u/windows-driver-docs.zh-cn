---
Description: 本主题中你将使用随 Microsoft Visual Studio Professional 2019 提供 USB 内核模式驱动程序模板编写简单的内核模式驱动程序框架 (KMDF) 的基于客户端驱动程序。
title: 如何编写第一个 USB 客户端驱动程序 (KMDF)
ms.date: 06/07/2019
ms.localizationpriority: medium
ms.openlocfilehash: 36c4ab490118f72610ec52837e014334ca77c9c6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67368790"
---
# <a name="how-to-write-your-first-usb-client-driver-kmdf"></a>如何编写第一个 USB 客户端驱动程序 (KMDF)


本主题中将使用**USB 内核模式驱动程序**提供与 Microsoft Visual Studio Professional 2019 编写简单的内核模式驱动程序框架 (KMDF) 模板-基于客户端驱动程序。 生成并安装客户端驱动程序之后, 您将查看中的客户端驱动程序**设备管理器**并在调试器中查看驱动程序输出。

由模板生成的源代码的说明，请参阅[了解 USB 客户端驱动程序的 KMDF 模板代码](understanding-the-kmdf-template-code-for-usb.md)。

### <a name="prerequisites"></a>先决条件

有关开发、 调试和安装的内核模式驱动程序，需要两台计算机：

-   运行 Windows 7 或更高版本的 Windows 操作系统的主机计算机。 在主计算机是开发环境中，可以编写和调试您的驱动程序。
-   运行 Windows Vista 或更高版本的 Windows 的目标计算机。 目标计算机具有你想要调试的内核模式驱动程序。

在开始之前，请确保满足以下要求：

**软件要求**

-   在主计算机承载你的开发环境，并具有 Visual Studio Professional 2019。
-   主机计算机包含 Windows 8 的最新的 Windows Driver Kit (WDK)。 该工具包包括标头、 库、 工具、 文档和开发，所需的调试工具生成和调试 KMDF 驱动程序。 若要获取最新版本的 WDK，请参阅[下载 Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。
-   在主计算机具有最新版本的 Windows 调试工具。 可以从 WDK 中获取最新版本也可以[下载和为 Windows 中安装调试的工具](https://msdn.microsoft.com/windows/hardware/gg463009.aspx)。
-   在目标计算机正在运行 Windows Vista 或更高版本的 Windows。
-   在主机和目标计算机配置为内核调试。 有关详细信息，请参阅[设置网络连接在 Visual Studio 中](https://docs.microsoft.com/windows-hardware/drivers/debugger/setting-up-a-network-debugging-connection-in-visual-studio)。

**硬件要求**

获取为其编写客户端驱动程序的 USB 设备。 在大多数情况下，则会使用 USB 设备和其硬件规范。 此规范描述设备功能和受支持的供应商命令。 使用规范来确定 USB 驱动程序和相关的设计决策的功能。

如果您不熟悉 USB 驱动程序开发，使用 OSR USB FX2 学习工具包来研究附带 WDK 的 USB 示例。 就可以从学习工具包[OSR 联机](http://www.osronline.com/)。 它包含 USB FX2 设备和所有所需的硬件规范来实现客户端驱动程序。

此外可以获取 Microsoft USB 测试工具 (MUTT) 设备。 可以从购买 MUTT 硬件[JJG 技术](http://jjgtechnologies.com/mutt.md)。 设备没有安装的已安装的固件。 若要安装固件，下载从 MUTT 软件包[此网站](https://msdn.microsoft.com/windows/hardware/jj590752)并运行 MUTTUtil.exe。 有关详细信息，请参阅随程序包提供的文档。

**推荐的读物**

-   [对所有驱动程序开发人员概念](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/concepts-and-knowledge-for-all-driver-developers)
-   [设备节点和设备堆栈](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)
-   [Windows 驱动程序入门](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/index)
-   [内核模式驱动程序框架](https://docs.microsoft.com/windows-hardware/drivers/wdf/)
-   *使用 Windows Driver Foundation 开发驱动程序*、 由 Penny Orwick 和 Smith 专家编写。 有关详细信息，请参阅[开发驱动程序与 WDF](https://msdn.microsoft.com/windows/hardware/gg463318)。

<a name="instructions"></a>说明
------------

### <a href="" id="generate-the-kmdf-driver-code-by-using-the--visual-studio-professional-2019---usb-driver-template"></a>步骤 1:通过使用 Visual Studio Professional 2019 USB 驱动程序模板生成 KMDF 驱动程序代码

有关生成 KMDF 驱动程序代码的说明，请参阅中的步骤[编写 KMDF 驱动程序基于模板](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/writing-a-kmdf-driver-based-on-a-template)。

**对于特定于 USB 的代码，选择以下选项在 Visual Studio Professional 2019**

1.  在中**新的项目**对话框中，在搜索框中，在顶部，类型**USB。**
2.  在中间窗格中，选择**内核模式驱动程序、 USB (KMDF)** 。
3.  单击“下一步”。
4.  输入项目名称，选择保存位置，然后单击**创建**。

以下屏幕截图显示**新的项目**对话框**USB 内核模式驱动程序**模板。

![visual studio 新项目选项](images/kmdf-template-visual-studio-2019.png)

![visual studio 新项目选项第二个屏幕](images/kmdf-template-visual-studio-2019-2.png)

本主题假定 Visual Studio 项目的名称为"MyUSBDriver\_"。 它包含以下文件：

| 文件                      | 描述                                                                                                          |
|----------------------------|----------------------------------------------------------------------------------------------------------------------|
| Public.h                   | 提供的与 USB 设备进行通信的客户端驱动程序和用户应用程序共享的常见声明。 |
| *&lt;项目名称&gt;* .inf | 包含在目标计算机上安装客户端驱动程序所需的信息。                                   |
| Trace.h                    | 声明跟踪函数和宏。                                                                               |
| Driver.h;Driver.c         | 声明和定义驱动程序入口点和事件回调例程。                                                |
| Device.h;Device.c         | 声明和定义用于准备-硬件事件的事件回调例程。                                          |
| Queue.h;Queue.c           | 声明和定义由框架的队列对象引发的事件的事件回调例程。                 |

 

### <a href="" id="modify-the-inf-file-to-add-information-about-your-device"></a>步骤 2:修改要添加你的设备有关的信息的 INF 文件

生成该驱动程序之前，必须了解你的设备，专门的硬件 ID 字符串修改模板 INF 文件的信息。

在中**解决方案资源管理器**下**驱动程序文件**，双击 INF 文件。

INF 文件中可以提供信息，例如制造商和提供程序名称，设备安装程序类中，依次类推。 必须提供的一个事项是设备的信息的你的硬件标识符。

若要提供的硬件 ID 字符串：

1.  将 USB 设备连接到主计算机，让 Windows 设备枚举。
2.  打开**设备管理器**并打开你的设备的属性。
3.  上**详细信息**选项卡上，选择**Id**下**属性。**

    设备的硬件 ID 显示在列表框中。 右键单击并复制硬件 ID 字符串。

4.  将 USB\\VID\_vvvv & PID\_pppp 在以下行中的硬件 ID 字符串。

    `[Standard.NT$ARCH$] %MyUSBDriver_.DeviceDesc%=MyUSBDriver__Device, USB\VID_vvvv&PID_pppp`

### <a href="" id="build-the-usb-client-driver-code"></a>步骤 3:生成 USB 客户端驱动程序代码

**若要构建您的驱动程序**

1.  在 Visual Studio Professional 2019 中打开驱动程序项目或解决方案
2.  右键单击该解决方案中的**解决方案资源管理器**，然后选择**Configuration Manager**。
3.  从**Configuration Manager**，选择**活动解决方案配置**(例如， **Windows 8 调试**或**Windows 8 版本**) 和**活动解决方案平台**(例如，Win32) 对应于你感兴趣的生成的类型。
4.  从**构建**菜单上，单击**生成解决方案**。

有关详细信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

### <a href="" id="configure-a-computer-for-testing-and-debugging"></a>步骤 4:将计算机配置为进行测试和调试

若要测试和调试驱动程序，请在主计算机和目标计算机上的驱动程序上运行调试器。 到目前为止，已在主计算机上使用 Visual Studio 以生成驱动程序。 接下来需要配置目标计算机。 若要配置目标计算机，请按照中的说明[预配的计算机的驱动程序部署和测试](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

### <a href="" id="enable-tracing-for-kernel-debugging"> </a>步骤 5:启用内核调试跟踪

模板代码包含几条跟踪消息 (TraceEvents)，可以帮助您跟踪函数调用。 所有函数的源代码中都包含标记的入口和出口的例程的跟踪消息。 对于错误，跟踪消息包含错误代码和有意义的字符串。 为您的驱动程序项目启用了 WPP 跟踪，因为在生成过程中创建的 PDB 符号文件包含跟踪的消息格式的说明。 如果配置 WPP 跟踪的主机和目标计算机，您的驱动程序可以将跟踪消息发送到一个文件或调试器。

**若要配置主机计算机中的 WPP 跟踪**

1. 通过提取跟踪的消息格式中的 PDB 符号文件的说明创建跟踪消息格式 (TMF) 文件。

   Tracepdb.exe 可用于创建 TMF 文件。 该工具位于<em>&lt;安装文件夹&gt;</em>Windows 工具包\\8.0\\bin\\ *&lt;体系结构&gt;* WDK 的文件夹。 以下命令创建的驱动程序项目的 TMF 文件。

   **tracepdb -f \[PDBFiles\] -p \[TMFDirectory\]**

   **-F**选项指定的位置和 PDB 符号文件的名称。 **-P**选项指定创建的 Tracepdb TMF 文件的位置。 有关详细信息，请参阅[ **Tracepdb 命令**](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracepdb-commands)。

   在指定位置中，你将看到三个文件 （.cpp 文件的项目中每一个）。 系统会提供 GUID 文件的名称。

2. 在调试器中，键入以下命令：
   1.  **.load Wmitrace**

       加载 Wmitrace.dll 扩展。

   2.  **.chain**

       验证加载调试程序扩展。

   3.  * *！ wmitrace.searchpath + * * *&lt;TMF 文件位置&gt;*

       将 TMF 文件的位置添加到调试器扩展的搜索路径。

       输出类似于下面这样：

       `Trace Format search path is: 'C:\Program Files (x86)\Microsoft Visual Studio 14.0\Common7\IDE;c:\drivers\tmf'`

**若要配置目标计算机中的 WPP 跟踪**

1. 请确保在目标计算机上具有跟踪日志工具。 该工具位于<em>&lt;安装\_文件夹&gt;</em>Windows 工具包\\8.0\\工具\\ *&lt;arch&gt;*  WDK 的文件夹。 有关详细信息，请参阅[ **Tracelog 命令语法**](https://docs.microsoft.com/windows-hardware/drivers/devtest/tracelog-command-syntax)。
2. 打开**命令窗口**并以管理员身份运行。
3. 键入下列命令：

   **tracelog-启动 MyTrace guid \#c918ee71-68c7-4140-8f7d-c907abbcb05d-标志 0xFFFF-级别 7 rt kd**

   该命令启动名为 MyTrace 跟踪会话。

   **Guid**参数指定的跟踪提供程序，这是客户端驱动程序的 GUID。 在 Visual Studio Professional 2019 项目中，可以从 Trace.h 获取 GUID。 作为另一个选项，可以键入以下命令，并在.guid 文件中指定的 GUID。 该文件包含连字符格式的 GUID:

   **tracelog-启动 MyTrace-guid c:\\驱动程序\\Provider.guid-标志 0xFFFF-级别 7 rt kd**

   可以通过键入以下命令来停止跟踪会话：

   **tracelog -stop MyTrace**

### <a href="" id="deploy-the-driver-on-the-target-computer"></a>步骤 6:部署目标计算机上的驱动程序

1. 在中**解决方案资源管理器**窗口中，右键单击<em>&lt;项目名称&gt;</em>**包**，然后选择**属性**.
2. 在左窗格中，导航到**配置属性&gt;驱动程序安装&gt;部署**。
3. 检查启用部署，并选中导入到驱动程序存储区。
4. 有关**远程计算机名称**，指定目标计算机的名称。
5. 选择**安装并验证**。
6. 单击“确定”。
7. 在**调试**菜单上，选择**开始调试**或按键盘上的 **F5**。

**请注意**  不要*不*指定在设备的硬件 ID**硬件 ID 的驱动程序更新**。 必须仅在您的驱动程序的信息 (INF) 文件中指定的硬件 ID。

 

有关部署到目标系统中 Visual Studio Professional 2019 驱动程序的详细信息，请参阅[部署到测试计算机的驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。

您还可以手动安装该驱动程序在目标计算机上使用设备管理器。 如果你想要在命令提示符下安装驱动程序，提供了这些实用程序：

-   [PnPUtil](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil)

    此工具附带于 Windows。 处于 Windows\\System32。 此实用程序可用于将驱动程序添加到驱动程序存储区。

    ```cmd
    C:\>pnputil /a m:\MyDriver_.inf
    Microsoft PnP Utility

    Processing inf : MyDriver_.inf
    Driver package added successfully.
    Published name : oem22.inf
    ```

    有关详细信息，请参阅[PnPUtil 示例](https://docs.microsoft.com/windows-hardware/drivers/devtest/pnputil-examples)。

-   [**DevCon 更新**](https://docs.microsoft.com/windows-hardware/drivers/devtest/devcon-update)

    此工具附带了 WDK。 可以使用它来安装和更新驱动程序。

    ```cmd
    devcon update c:\windows\inf\MyDriver_.inf USB\VID_0547&PID_1002\5&34B08D76&0&6
    ```

### <a href="" id="view-the-driver-in-device-manager"></a>步骤 7:查看设备管理器中的驱动程序

1.  输入以下命令以打开**设备管理器**:

    **devmgmt**

2.  确认**设备管理器**显示以下节点的节点：

    **示例**

    **MyUSBDriver\_Device**

### <a href="" id="view-the-output-in-the-debugger"></a>步骤 8:在调试器中查看输出

Visual Studio 将首先显示正在**输出**窗口。 然后它将打开**调试程序即时窗口**。 验证跟踪消息显示在主机计算机上的调试器。 输出应如下所示，其中"MyUSBDriver\_"的驱动程序模块名称：

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