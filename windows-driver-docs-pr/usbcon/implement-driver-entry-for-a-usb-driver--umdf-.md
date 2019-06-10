---
Description: 使用 Microsoft Visual Studio 提供的 USB 用户模式驱动程序模板可用于编写 UMDF 客户端驱动程序。
title: 如何编写第一个 USB 客户端驱动程序 (UMDF)
ms.date: 06/03/2019
ms.localizationpriority: medium
ms.openlocfilehash: b6dc3fa4802deb3a028aef7545cae6ee5e7c9cad
ms.sourcegitcommit: 2589492f3c14f779efa8b446e81d4e0f6d048f4f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/08/2019
ms.locfileid: "66815101"
---
# <a name="how-to-write-your-first-usb-client-driver-umdf"></a>如何编写第一个 USB 客户端驱动程序 (UMDF)


本主题中将使用**USB 用户模式驱动程序**提供与 Microsoft Visual Studio 2019 编写用户模式驱动程序框架 (UMDF) 模板-基于客户端驱动程序。 生成并安装客户端驱动程序之后, 您将查看中的客户端驱动程序**设备管理器**并在调试器中查看驱动程序输出。

UMDF （称为本主题中的框架） 基于组件对象模型 (COM)。 每个框架对象必须实现[ **IUnknown** ](https://msdn.microsoft.com/library/windows/desktop/ms680509)及其方法[ **QueryInterface**](https://msdn.microsoft.com/library/windows/desktop/ms682521)， [ **AddRef**](https://msdn.microsoft.com/library/windows/desktop/ms691379)，并[**发行**](https://msdn.microsoft.com/library/windows/desktop/ms682317)，默认情况下。 **AddRef**并**发行**方法管理对象的生存期，因此，客户端驱动程序不需要维护的引用计数。 **QueryInterface**方法，客户端驱动程序与其他框架对象的接口指针获取 Windows 驱动程序框架 (WDF) 对象模型中。 Framework 对象执行复杂的驱动程序任务，并与 Windows 进行交互。 某些 framework 对象公开启用客户端驱动程序与框架进行交互的接口。

作为进程内 COM 服务器 (DLL) 实现 UMDF 基于客户端驱动程序和C++是用于编写 USB 设备的客户端驱动程序的首选的语言。 通常情况下，客户端驱动程序实现多个由框架公开的接口。 本主题是指一个回调类作为实现 framework 接口的客户端驱动程序定义类。 这些类进行实例化后，将生成的回调对象是与特定的框架对象合作。 这种合作关系使客户端驱动程序有机会对设备或报告的框架的系统相关事件进行响应。 每当 Windows 会通知框架，有关特定事件，框架将调用客户端驱动程序的回调，如果有可用。 否则，该框架将继续进行事件的默认处理。 模板代码定义驱动程序、 设备和队列回调类。

由模板生成的源代码的说明，请参阅[了解 USB 客户端驱动程序的 UMDF 模板代码](understanding-the-umdf-template-code-for-usb.md)。

### <a name="prerequisites"></a>先决条件

有关开发、 调试和安装的用户模式驱动程序，需要两台计算机：

-   运行 Windows 7 或更高版本的 Windows 操作系统的主机计算机。 在主计算机是开发环境中，可以编写和调试您的驱动程序。
-   想要测试您的驱动程序，例如，Windows 10，版本 1903年上运行的操作系统版本的目标计算机。 目标计算机具有你想要调试的用户模式驱动程序和一个调试器。

在某些情况下，在主机和目标计算机运行相同版本的 Windows，您可以只需一台运行 Windows 7 或更高版本的 Windows 计算机。 本主题假定你使用的开发、 调试和安装用户模式驱动程序的两个计算机。

在开始之前，请确保满足以下要求：

**软件要求**

-   在主计算机具有 Visual Studio 2019。
-   在主计算机具有最新的 Windows Driver Kit (WDK) 适用于 Windows 10，版本 1903年。

    该工具包包括标头、 库、 工具、 文档和开发，所需的调试工具生成和调试 USB 客户端驱动程序。 可以获取最新版本从 WDK[如何获取 WDK](https://go.microsoft.com/fwlink/p/?linkid=617585)。

-   在主计算机具有最新版本的 Windows 调试工具。 可以从 WDK 中获取最新版本也可以[下载和为 Windows 中安装调试的工具](https://go.microsoft.com/fwlink/p/?linkid=617701)。
-   如果使用两台计算机，则必须配置用于用户模式下调试的主机和目标计算机。 有关详细信息，请参阅[设置用户模式下调试在 Visual Studio 中](https://msdn.microsoft.com/library/windows/hardware/hh439381)。

**硬件要求**

获取为其编写客户端驱动程序的 USB 设备。 在大多数情况下，则会使用 USB 设备和其硬件规范。 此规范描述设备功能和受支持的供应商命令。 使用规范来确定 USB 驱动程序和相关的设计决策的功能。

如果您不熟悉 USB 驱动程序开发，使用 OSR USB FX2 学习工具包来研究附带 WDK 的 USB 示例。 就可以从学习工具包[OSR 联机](https://go.microsoft.com/fwlink/p/?linkid=617553)。 它包含 USB FX2 设备和所有所需的硬件规范来实现客户端驱动程序。

**推荐的读物**

-   [对所有驱动程序开发人员概念](https://msdn.microsoft.com/library/windows/hardware/ff554731)
-   [设备节点和设备堆栈](https://msdn.microsoft.com/library/windows/hardware/ff554721)
-   [Windows 驱动程序入门](https://msdn.microsoft.com/library/windows/hardware/ff554690)
-   [用户模式驱动程序框架](https://msdn.microsoft.com/library/windows/hardware/ff560027)
-   *使用 Windows Driver Foundation 开发驱动程序*、 由 Penny Orwick 和 Smith 专家编写。 有关详细信息，请参阅[开发驱动程序与 WDF](https://go.microsoft.com/fwlink/p/?linkid=617702)。

<a name="instructions"></a>说明
------------

### <a href="" id="generate-the-umdf-driver-code-by-using-the-visual-studio-2019-usb-driver-template"></a>步骤 1:通过使用 Visual Studio 2019 USB 驱动程序模板生成 UMDF 驱动程序代码

<a href="" id="generate"></a> 有关生成 UMDF 驱动程序代码的说明，请参阅[编写 UMDF 驱动程序基于模板](https://msdn.microsoft.com/library/windows/hardware/hh439659)。

**对于特定于 USB 的代码，选择以下选项在 Visual Studio 2019**

1.  在中**新的项目**对话框中，在搜索框中，在顶部，类型**USB。**
2.  在中间窗格中，选择**用户模式驱动程序，USB (UMDF V2)** 。
3.  单击“下一步”  。
4.  输入项目名称，选择保存位置，然后单击**创建**。

以下屏幕截图显示**新的项目**对话框**USB 用户模式驱动程序**模板。

![visual studio 新项目选项](images/umdf-template-visual-studio-2019.png)

![visual studio 新项目选项第二个屏幕](images/umdf-template-visual-studio-2019-2.png)

本主题假定项目的名称为"MyUSBDriver\_UMDF\_"。 它包含以下文件：

| 文件                      | 描述                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|----------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Driver.h;Driver.c         | 声明和定义实现一个回调类[ **IDriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff554885)接口。 类定义由 framework 驱动程序对象调用的方法。 此类的主要用途是创建客户端驱动程序的设备对象。                                                                                                                                                                     |
| Device.h;Device.c         | 声明和定义实现一个回调类[ **IPnpCallbackHardware** ](https://msdn.microsoft.com/library/windows/hardware/ff556764)接口。 类定义由 framework 设备对象调用的方法。 此类的主要目的是处理由于插 (PnP) 状态的更改而发生的事件。 类还分配并初始化所需的客户端驱动程序，只要它加载到系统中的资源。 |
| IoQueue.h;IoQueue.c       | 声明和定义实现一个回调类[ **IQueueCallbackDeviceIoControl** ](https://msdn.microsoft.com/library/windows/hardware/ff556852)接口。 类定义由 framework 队列对象调用的方法。 此类的目的是检索在框架中排队的 I/O 请求。                                                                                                                               |
| internal.h                 | 提供的与 USB 设备进行通信的客户端驱动程序和用户应用程序共享的常见声明。 它还声明跟踪函数和宏。                                                                                                                                                                                                                                                                          |
| Dllsup.cpp                 | 包含驱动程序模块的入口点的实现。                                                                                                                                                                                                                                                                                                                                                                              |
| *&lt;项目名称&gt;* .inf | 在目标计算机上安装客户端驱动程序所需的 INF 文件。                                                                                                                                                                                                                                                                                                                                                               |
| Exports.def                | DEF 文件导出入口点的驱动程序模块的函数名称。                                                                                                                                                                                                                                                                                                                                                                    |

 

### <a href="" id="modify-the-inf-file-to-add-information-about-your-device"></a>步骤 2:修改要添加你的设备有关的信息的 INF 文件

<a href="" id="modify"></a> 生成该驱动程序之前，必须了解你的设备，专门的硬件 ID 字符串修改模板 INF 文件的信息。

**若要提供的硬件 ID 字符串**

1.  将 USB 设备连接到主计算机，让 Windows 设备枚举。
2.  打开**设备管理器**并打开你的设备的属性。
3.  上**详细信息**选项卡上，选择**Id**下**属性。**

    设备的硬件 ID 显示在列表框中。 右键单击并复制硬件 ID 字符串。

4.  在中**解决方案资源管理器**，展开**驱动程序文件**，并打开 INF。
5.  之后的替换为你的硬件 ID 的字符串。

    `[Standard.NT$ARCH$]`

    `%DeviceName%=MyDevice_Install, USB\VID_vvvv&PID_pppp`

请注意**AddReg**驱动程序的信息 (INF) 文件中的条目。

`[CoInstallers_AddReg] ;`

`HKR,,CoInstallers32,0x00010008,"WudfCoinstaller.dll"`

`HKR,,CoInstallers32,0x00010008,"WudfUpdate_01011.dll"`

`HKR,,CoInstallers32,0x00010008,"WdfCoInstaller01011.dll,WdfCoInstaller"`

`HKR,,CoInstallers32,0x00010008,"WinUsbCoinstaller2.dll"`

- WudfCoinstaller.dll （配置共同安装程序）
- WUDFUpdate\_ *&lt;版本&gt;* .dll （可再发行组件共同安装程序）
- Wdfcoinstaller<em>&lt;版本&gt;</em>.dll （对于 KMDF 共同安装程序）
- Winusbcoinstaller2.dll （（共同安装程序为 Winusb.sys）
- MyUSBDriver\_UMDF\_.dll （客户端驱动程序模块）

如果 INF AddReg 指令引用 UMDF 可再发行组件共同安装程序 (WUDFUpdate\_ *&lt;版本&gt;* .dll)，您必须进行配置辅助安装程序 （的引用WUDFCoInstaller.dll)。 引用 INF 中的这两个共同安装程序将导致安装错误。

所有基于 UMDF 的 USB 客户端驱动程序需要两个由 Microsoft 提供的驱动程序： 反射和 WinUSB。

-   反射器 — 如果您的驱动程序已成功获取加载，作为内核模式堆栈中的最顶层的驱动程序加载该发送程序。 该发送程序必须在内核模式堆栈顶部的驱动程序。 若要满足此要求，模板的 INF 文件即服务和 WinUSB 作为低筛选器驱动程序 INF 中指定该发送程序：

    `[MyDevice_Install.NT.Services]`

    `AddService=WUDFRd,0x000001fa,WUDFRD_ServiceInstall  ; flag 0x2 sets this as the service for the device`

    `AddService=WinUsb,0x000001f8,WinUsb_ServiceInstall  ; this service is installed because its a filter.`

-   WinUSB — 安装包必须包含为 Winusb.sys 共同安装程序，因为对于客户端驱动程序，WinUSB 为网关到内核模式 USB 驱动程序堆栈。 获取加载的另一个组件是名 WinUsb.dll，为在客户端驱动程序的主机进程 (Wudfhost.exe) 的用户模式 DLL。 公开 Winusb.dll [WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)，简化客户端驱动程序和 WinUSB 之间的通信过程。

### <a href="" id="build-the-usb-client-driver-code"></a>步骤 3:生成 USB 客户端驱动程序代码

<a href="" id="build"></a>
**若要构建您的驱动程序**

1.  在 Visual Studio 2019 中打开驱动程序项目或解决方案。
2.  右键单击该解决方案中的**解决方案资源管理器**，然后选择**Configuration Manager**。
3.  从**Configuration Manager**，选择你**活动解决方案配置**(例如，**调试**或**版本**) 和你**活动解决方案平台**(例如， **Win32**) 对应于你感兴趣的生成的类型。
4.  验证你的设备接口的 GUID 准确在整个项目。 
    - 设备接口的 GUID Trace.h 中定义并从引用`MyUSBDriverUMDFCreateDevice`Device.c 中。 在创建你的项目具有名称"MyUSBDriver\_UMDF\_"，Visual Studio 2019 定义设备接口的 GUID with 名称`GUID_DEVINTERFACE_MyUSBDriver_UMDF_`，但调用`WdfDeviceCreateDeviceInterface`with 不正确的参数"GUID_DEVINTERFACE_MyUSBDriverUMDF"。 不正确的参数替换 Trace.h 以确保该驱动程序正确生成中定义的名称。 
4.  从**构建**菜单上，单击**生成解决方案**。

有关详细信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

### <a href="" id="configure-a-computer-for-testing-and-debugging"></a>步骤 4:将计算机配置为进行测试和调试

若要测试和调试驱动程序，请在主计算机和目标计算机上的驱动程序上运行调试器。 到目前为止，已在主计算机上使用 Visual Studio 以生成驱动程序。 接下来需要配置目标计算机。 若要配置目标计算机，请按照中的说明[预配的计算机的驱动程序部署和测试](https://msdn.microsoft.com/library/windows/hardware/dn745909)。

### <a href="" id="enable-tracing-for-kernel-debugging"> </a>步骤 5:启用内核调试跟踪

模板代码包含几条跟踪消息 (TraceEvents)，可以帮助您跟踪函数调用。 所有函数的源代码中都包含标记的入口和出口的例程的跟踪消息。 对于错误，跟踪消息包含错误代码和有意义的字符串。 为您的驱动程序项目启用了 WPP 跟踪，因为在生成过程中创建的 PDB 符号文件包含跟踪的消息格式的说明。 如果配置 WPP 跟踪的主机和目标计算机，您的驱动程序可以将跟踪消息发送到一个文件或调试器。

**若要配置主机计算机中的 WPP 跟踪**

1. 通过提取跟踪的消息格式中的 PDB 符号文件的说明创建跟踪消息格式 (TMF) 文件。

   Tracepdb.exe 可用于创建 TMF 文件。 该工具位于<em>&lt;安装文件夹&gt;</em>Windows 工具包\\10\\bin\\ *&lt;体系结构&gt;* WDK 的文件夹。 以下命令创建的驱动程序项目的 TMF 文件。

   **tracepdb -f \[PDBFiles\] -p \[TMFDirectory\]**

   **-F**选项指定的位置和 PDB 符号文件的名称。 **-P**选项指定创建的 Tracepdb TMF 文件的位置。 有关详细信息，请参阅[ **Tracepdb 命令**](https://msdn.microsoft.com/library/windows/hardware/ff553043)。

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

1. 请确保在目标计算机上具有跟踪日志工具。 该工具位于<em>&lt;安装\_文件夹&gt;</em>Windows 工具包\\10\\工具\\ *&lt;arch&gt;*  WDK 的文件夹。 有关详细信息，请参阅[ **Tracelog 命令语法**](https://msdn.microsoft.com/library/windows/hardware/ff553012)。
2. 打开**命令窗口**并以管理员身份运行。
3. 键入下列命令：

   **tracelog-启动 MyTrace guid \#c918ee71-68c7-4140-8f7d-c907abbcb05d-标志 0xFFFF-级别 7 rt kd**

   该命令启动名为 MyTrace 跟踪会话。

   **Guid**参数指定的跟踪提供程序，这是客户端驱动程序的 GUID。 在 Visual Studio 2019 项目中，可以从 Trace.h 获取 GUID。 作为另一个选项，可以键入以下命令，并在.guid 文件中指定的 GUID。 该文件包含连字符格式的 GUID:

   **tracelog-启动 MyTrace-guid c:\\驱动程序\\Provider.guid-标志 0xFFFF-级别 7 rt kd**

   可以通过键入以下命令来停止跟踪会话：

   **tracelog -stop MyTrace**

### <a href="" id="deploy-the-driver-on-the-target-computer"></a>步骤 6:部署目标计算机上的驱动程序

1. 在中**解决方案资源管理器**窗口中，右键单击<em>&lt;项目名称&gt;</em>**包**，然后选择**属性**.
2. 在左窗格中，导航到**配置属性&gt;驱动程序安装&gt;部署**。
3. 检查启用部署，并选中导入到驱动程序存储区。
4. 有关**远程计算机名称**，指定目标计算机的名称。
5. 选择**安装并验证**。
6. 单击“确定”  。
7. 在**调试**菜单上，选择**开始调试**或按键盘上的 **F5**。

**请注意**  不要*不*指定在设备的硬件 ID**硬件 ID 的驱动程序更新**。 必须仅在您的驱动程序的信息 (INF) 文件中指定的硬件 ID。

 

### <a href="" id="view-the-driver-in-device-manager"></a>步骤 7:查看设备管理器中的驱动程序

<a href="" id="devicemanager"></a>
1.  输入以下命令以打开**设备管理器**。

    **devmgmt**

2.  确认**设备管理器**显示了以下节点。

    **USB 设备**

    **MyUSBDriver\_UMDF\_Device**

### <a href="" id="view-the-output-in-the-debugger"></a>步骤 8:在调试器中查看输出

验证是否在显示跟踪消息**调试程序即时窗口**主机计算机上。

输出应类似于下面。

``` syntax
[0]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::OnPrepareHardware Entry
[0]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::OnPrepareHardware Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::CreateInstanceAndInitialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Initialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Initialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::CreateInstanceAndInitialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Configure Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::CreateInstanceAndInitialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::Initialize Entry
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::Initialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyIoQueue::CreateInstanceAndInitialize Exit
[1]0744.05F0::00/00/0000-00:00:00.000 [MyUSBDriver_UMDF_]CMyDevice::Configure Exit
```

<a name="remarks"></a>备注
-------

让我们看一看框架和客户端驱动程序如何协同工作以与 Windows 进行交互并处理请求发送到 USB 设备。 此图显示了为 UMDF 系统中加载的模块-基于 USB 客户端驱动程序。

![用户模式下客户端驱动程序体系结构](images/umdfstack.png)

下面说明了每个模块的用途：

-   应用程序 — 用户模式进程，它会发出 I/O 请求与 USB 设备进行通信。
-   I/O 管理器-创建 I/O 请求数据包 (Irp) 来表示接收应用程序请求，并将其转发到的目标设备的内核模式设备堆栈顶部的 Windows 组件。
-   反射器 — 顶部的内核模式设备堆栈 (WUDFRd.sys) 安装了 Microsoft 提供的内核模式驱动程序。 该发送程序将 Irp I/O 管理器从接收到客户端驱动程序主机进程重定向。 收到请求后，框架和客户端驱动程序处理请求。
-   主机进程，在其中用户模式驱动程序运行 (Wudfhost.exe) 的进程。 它还托管框架和 I/O 调度程序。
-   客户端驱动程序 — USB 设备的用户模式下函数驱动程序。
-   UMDF — 处理大多数的与交互 Windows 代表客户端驱动程序的框架模块。 它公开客户端驱动程序可用于执行常见的驱动程序任务的用户模式设备驱动程序接口 (DDIs)。
-   调度程序 — 在主机进程; 中运行的机制确定如何将请求转发给内核模式后它已被用户模式驱动程序处理，并且已达到用户模式堆栈的底部。 在图中，调度程序将请求转发到用户模式 DLL，Winusb.dll。
-   Microsoft 提供的用户模式 DLL 公开 Winusb.dll—a [WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)，简化客户端驱动程序和 WinUSB (Winusb.sys，在内核模式下加载) 之间的通信过程。
-   Winusb.sys—a Microsoft 提供的驱动程序所需的 USB 设备的所有 UMDF 客户端驱动程序。 该驱动程序必须作为网关到内核模式中的 USB 驱动程序堆栈安装下面的反射和行为。 有关详细信息，请参阅[WinUSB](winusb.md)。
-   USB 驱动程序堆栈-一组处理驱动程序，Microsoft 提供的协议级别的通信使用 USB 设备。 有关详细信息，请参阅[USB 宿主端驱动程序在 Windows 中的](usb-3-0-driver-stack-architecture.md)。

每当应用程序发出请求的 USB 驱动程序堆栈，Windows I/O 管理器将请求发送到反射器，将其定向到在用户模式下的客户端驱动程序。 客户端驱动程序处理该请求是通过调用特定 UMDF 方法，在内部调用[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)将请求发送到 WinUSB。 收到请求后，WinUSB 处理请求或将其转发到 USB 驱动程序堆栈。

## <a name="related-topics"></a>相关主题
[了解 USB 客户端驱动程序的 UMDF 模板代码](understanding-the-umdf-template-code-for-usb.md)  
[如何启用 USB 选择性挂起和系统唤醒 USB 设备在 UMDF 驱动程序中](https://go.microsoft.com/fwlink/p/?linkid=617587)  
[USB 客户端驱动程序开发入门](getting-started-with-usb-client-driver-development.md)  



