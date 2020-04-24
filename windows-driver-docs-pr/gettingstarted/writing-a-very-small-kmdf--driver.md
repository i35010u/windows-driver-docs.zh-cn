---
title: 编写通用 Hello World 驱动程序 (KMDF)
description: 本主题介绍了如何使用内核模式驱动程序框架 (KMDF) 编写通用 Windows 驱动程序。 首先使用 Microsoft Visual Studio 模板，然后在单独的计算机上部署和安装你的驱动程序。
ms.assetid: B4200732-67B5-4BD9-8852-81387912A9A4
keywords:
- KMDF Hello World
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: d4e8ef4e012d9f09ec0b60bad6bc2910a1ce253b
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "81679416"
---
# <a name="write-a-universal-hello-world-driver-kmdf"></a>编写通用 Hello World 驱动程序 (KMDF)


本主题介绍了如何使用内核模式驱动程序框架 (KMDF) 编写非常小的[通用 Windows 驱动程序](https://docs.microsoft.com/windows-hardware/drivers)，然后在单独的计算机上部署并安装驱动程序。 

若要开始操作，请确保已安装 [Microsoft Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=698539)、[Windows SDK](https://developer.microsoft.com/windows/downloads/windows-10-sdk) 和 [Windows 驱动程序工具包 (WDK)](https://go.microsoft.com/fwlink/p/?LinkId=733614)。

安装 WDK 时，需要包括 [Windows 调试工具](https://go.microsoft.com/fwlink/p?linkid=223405)。

## <a name="create-and-build-a-driver"></a>创建和生成驱动程序


1.  打开 Microsoft Visual Studio。 在“文件”  菜单上，选择“新建”&gt;“项目”  。
2.  在“新建项目”对话框的左侧窗格中，依次转到  “Visual C++”&gt;“Windows 驱动程序”&gt;“WDF”。
3.  在中间窗格中，选择“内核模式驱动程序，空(KMDF)”  。
4.  在“名称”  字段中，输入“KmdfHelloWorld”作为项目名称。

    > [!NOTE]
    > 在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。
     

5.  在“位置”  字段中，输入要在其中创建新项目的目录。
6.  选中“创建解决方案的目录”  。 单击“确定”  。

    ![“新建项目”对话框的屏幕截图](images/vs2015-new-project-kmdf-empty.png)

    Visual Studio 将创建一个项目和一个解决方案。 可以在“解决方案资源管理器”  窗口中看到它们，如此处所示。 （如果未显示“解决方案资源管理器”  窗口，请从“视图”  菜单中选择“解决方案资源管理器”。）该解决方案有一个名为 KmdfHelloWorld 的驱动程序项目。

    ![“解决方案资源管理器”窗口的屏幕截图，显示了解决方案和空的驱动程序项目 (kmdfhelloworld)](images/vs2015-kmdf-hello-world-solution-explorer.png)

7.  在“解决方案资源管理器”  窗口中，右键单击“KmdfHelloWorld”  项目，然后选择“属性”  。 导航到  “配置属性”&gt;“驱动程序设置”&gt;“常规”。请注意，“目标平台”  默认为“通用”  。  单击“取消”  。

8.  在“解决方案资源管理器”  窗口中，再次右键单击“KmdfHelloWorld”  项目，然后选择  “添加”&gt;“新项”。
9.  在“添加新项目”  对话框中，选择“C++ 文件”  。 对于“名称”  ，请输入“Driver.c”。

    > [!NOTE]
    > 文件扩展名为 **.c**，不是 **.cpp**。

     单击 **“添加”** 。 Driver.c 文件添加在源文件下，如下所示。

    ![“解决方案资源管理器”窗口的屏幕截图，显示添加到驱动程序项目中的 driver.c 文件](images/firstdriverkmdfsmall03.png)

## <a name="write-your-first-driver-code"></a>编写第一个驱动程序代码

创建空的 Hello World 项目并添加 Driver.c 源文件以后，即可通过实现两个基本事件回调函数来编写驱动程序运行所需的最基本的代码。 

1. 在 Driver.c 中，首先包括以下头文件：

    ```C++
    #include <ntddk.h>
    #include <wdf.h>
    ```

    [Ntddk.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk) 包含所有驱动程序的核心 Windows 内核定义，而 [Wdf.h](https://docs.microsoft.com/windows-hardware/drivers/ddi/_wdf) 包含基于 Windows 驱动程序框架 (WDF) 的驱动程序的定义。 

2. 接下来，为要使用的两个回调提供声明：

    ```C++
    DRIVER_INITIALIZE DriverEntry;
    EVT_WDF_DRIVER_DEVICE_ADD KmdfHelloWorldEvtDeviceAdd;
    ```

3. 使用以下代码编写 *DriverEntry*：

    ```C++
    NTSTATUS 
    DriverEntry(
        _In_ PDRIVER_OBJECT     DriverObject, 
        _In_ PUNICODE_STRING    RegistryPath
    )
    {
        // NTSTATUS variable to record success or failure
        NTSTATUS status = STATUS_SUCCESS;
        
        // Allocate the driver configuration object
        WDF_DRIVER_CONFIG config;
        
        // Print "Hello World" for DriverEntry
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: DriverEntry\n" ));

        // Initialize the driver configuration object to register the
        // entry point for the EvtDeviceAdd callback, KmdfHelloWorldEvtDeviceAdd
        WDF_DRIVER_CONFIG_INIT(&config, 
                               KmdfHelloWorldEvtDeviceAdd
                               );

        // Finally, create the driver object
        status = WdfDriverCreate(DriverObject, 
                                 RegistryPath, 
                                 WDF_NO_OBJECT_ATTRIBUTES, 
                                 &config, 
                                 WDF_NO_HANDLE
                                 );
        return status;
    }
    ```

    [*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 是所有驱动程序的入口点，就像 `Main()` 适用于许多用户模式应用程序一样。 *DriverEntry* 的任务是初始化驱动程序范围的结构和资源。 在此示例中，你针对 *DriverEntry* 输出了“Hello World”，将驱动程序对象配置为注册 *EvtDeviceAdd* 回调的入口点，然后创建了驱动程序对象并返回。 

    驱动程序对象充当你可能在驱动程序中创建的所有其他框架对象的父对象，这些框架对象包括设备对象、I/O 队列、计时器、旋转锁等。 有关框架对象的详细信息，请参阅[框架对象简介](../wdf/introduction-to-framework-objects.md)。

    > [!TIP]
    > 对于 *DriverEntry*，我们强烈建议将名称保留为“DriverEntry”，以便进行代码分析和调试。

4. 接下来，使用以下代码编写 *KmdfHelloWorldEvtDeviceAdd*：

    ```C++
    NTSTATUS 
    KmdfHelloWorldEvtDeviceAdd(
        _In_    WDFDRIVER       Driver, 
        _Inout_ PWDFDEVICE_INIT DeviceInit
    )
    {
        // We're not using the driver object,
        // so we need to mark it as unreferenced
        UNREFERENCED_PARAMETER(Driver);

        NTSTATUS status;

        // Allocate the device object
        WDFDEVICE hDevice;    

        // Print "Hello World"
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: KmdfHelloWorldEvtDeviceAdd\n" ));
        
        // Create the device object
        status = WdfDeviceCreate(&DeviceInit, 
                                 WDF_NO_OBJECT_ATTRIBUTES,
                                 &hDevice
                                 );
        return status;
    }
    ```

    系统在检测到你的设备已到达时，会调用 [*EvtDeviceAdd*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)。 它的任务是初始化该设备的结构和资源。 在此示例中，你仅针对 *EvtDeviceAdd* 输出了“Hello World”消息、创建了设备对象并返回。 在你编写的其他驱动程序中，可以为硬件创建 I/O 队列，为特定于设备的信息设置设备上下文  存储空间，或执行准备设备所需的其他任务。

    > [!TIP]
    > 对于设备添加回调，请注意以驱动程序名称为前缀对回调命名的方式 (*KmdfHelloWorld*EvtDeviceAdd)。 通常，我们建议以这种方式命名驱动程序功能，以区别于其他驱动程序的功能。 *DriverEntry* 是完全应该这样命名的唯一一项。

5. 现在，整个 Driver.c 如下所示：

    ```C++
    #include <ntddk.h>
    #include <wdf.h>
    DRIVER_INITIALIZE DriverEntry;
    EVT_WDF_DRIVER_DEVICE_ADD KmdfHelloWorldEvtDeviceAdd;

    NTSTATUS 
    DriverEntry(
        _In_ PDRIVER_OBJECT     DriverObject, 
        _In_ PUNICODE_STRING    RegistryPath
    )
    {
        // NTSTATUS variable to record success or failure
        NTSTATUS status = STATUS_SUCCESS;
        
        // Allocate the driver configuration object
        WDF_DRIVER_CONFIG config;
        
        // Print "Hello World" for DriverEntry
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: DriverEntry\n" ));

        // Initialize the driver configuration object to register the
        // entry point for the EvtDeviceAdd callback, KmdfHelloWorldEvtDeviceAdd
        WDF_DRIVER_CONFIG_INIT(&config, 
                               KmdfHelloWorldEvtDeviceAdd
                               );

        // Finally, create the driver object
        status = WdfDriverCreate(DriverObject, 
                                 RegistryPath, 
                                 WDF_NO_OBJECT_ATTRIBUTES, 
                                 &config, 
                                 WDF_NO_HANDLE
                                 );
        return status;
    }

    NTSTATUS 
    KmdfHelloWorldEvtDeviceAdd(
        _In_    WDFDRIVER       Driver, 
        _Inout_ PWDFDEVICE_INIT DeviceInit
    )
    {
        // We're not using the driver object,
        // so we need to mark it as unreferenced
        UNREFERENCED_PARAMETER(Driver);

        NTSTATUS status;

        // Allocate the device object
        WDFDEVICE hDevice;    

        // Print "Hello World"
        KdPrintEx(( DPFLTR_IHVDRIVER_ID, DPFLTR_INFO_LEVEL, "KmdfHelloWorld: KmdfHelloWorldEvtDeviceAdd\n" ));
        
        // Create the device object
        status = WdfDeviceCreate(&DeviceInit, 
                                 WDF_NO_OBJECT_ATTRIBUTES,
                                 &hDevice
                                 );
        return status;
    }
    ```

6. 保存 Driver.c。

此示例说明了驱动程序的基本概念：驱动程序是一个“回调集合”，经初始化后，会在系统有需要时等待系统调用。 这可能是新设备到达事件、用户模式应用程序的 I/O 请求、系统电源关闭事件、另一个驱动程序的请求，或用户意外拔出设备时的意外删除事件。 幸运的是，就“Hello World”而言，只需操心驱动程序和设备的创建。

接下来，将生成驱动程序。

## <a name="build-the-driver"></a>生成驱动程序

1. 在“解决方案资源管理器”  窗口中，右键单击“解决方案‘KmdfHelloWorld’(1 个项目)”  ，然后选择“配置管理器”  。 为驱动程序项目选择配置和平台。 在本练习中，我们选择“调试”和“x64”。  

2. 在“解决方案资源管理器”  窗口中，右键单击“KmdfHelloWorld”  ，然后选择“属性”  。 在  “Wpp 跟踪”&gt;“所有选项”中，将“运行 Wpp 跟踪”  设置为“否”  。 单击“应用”  ，然后单击“确定”  。
3. 若要生成驱动程序，请从“生成”  菜单中选择“生成解决方案”  。 Visual Studio 在“输出”  窗口中显示生成进度。 （如果“输出”  窗口不可见，请从“视图”  菜单中选择“输出”  。）验证解决方案成功生成后，即可关闭 Visual Studio。
4. 若要查看生成的驱动程序，则在“文件资源管理器”中，依次转到 **KmdfHelloWorld** 文件夹和 **C:\\KmdfHelloWorld\\x64\\Debug\KmdfHelloWorld**。 该文件夹包括：

    -   KmdfHelloWorld.sys - 内核模式驱动程序文件
    -   KmdfHelloWorld.inf - 在安装驱动程序时 Windows 使用的信息文件
    -   KmdfHelloWorld.cat - 安装程序验证驱动程序的测试签名所使用的目录文件


> [!TIP]
> 如果在生成驱动程序时看到 `DriverVer set to a date in the future`，则请更改驱动程序项目设置，让 Inf2Cat 设置 `/uselocaltime`。 为此，请使用  “配置属性”->“Inf2Cat”->“常规”->“使用本地时间”。 现在，[Stampinf](../devtest/stampinf-command-options.md) 和 Inf2Cat 都使用本地时间。

## <a name="span-iddeploy_the_driverspanspan-iddeploy_the_driverspanspan-iddeploy_the_driverspandeploy-the-driver"></a><span id="Deploy_the_driver"></span><span id="deploy_the_driver"></span><span id="DEPLOY_THE_DRIVER"></span>部署驱动程序

通常，在测试和调试驱动程序时，调试程序和驱动程序会在不同的计算机上运行。 运行调试程序的计算机称为“主计算机”  ，运行驱动程序的计算机称为“目标计算机”  。 目标计算机也称为“测试计算机”  。

到目前为止，你已在主计算机上使用 Visual Studio 生成了驱动程序。 现在，需要配置目标计算机。 

1. 按照[预配计算机以便进行驱动程序部署和测试 (WDK 10)](provision-a-target-computer-wdk-8-1.md) 中的说明进行操作。

    > [!TIP]
    > 按照步骤使用网络电缆自动预配目标计算机时，请记下端口和密钥。 以后，你将在调试步骤中使用它们。 在此示例中，我们将使用 **50000** 作为端口，使用 **1.2.3.4** 作为密钥。
    >
    > 在实际的驱动程序调试方案中，我们建议使用 KDNET 生成的密钥。 有关如何使用 KDNET 生成一个随机密钥的详细信息，请参阅[调试驱动程序 - 分步实验室（Sysvad 内核模式）](../debugger/debug-universal-drivers--kernel-mode-.md)主题。

2.  在主计算机上，在 Visual Studio 中打开你的解决方案。 可以在 KmdfHelloWorld 文件夹中双击解决方案文件 KmdfHelloWorld.sln。
3.  在“解决方案资源管理器”  窗口中，右键单击“KmdfHelloWorld”  项目，然后选择“属性”  。
4.  在“KmdfHelloWorld 属性页”  窗口中，转到“配置属性”&gt;“驱动程序安装”&gt;“部署”  ，如下所示。
5.  选中“部署前删除以前的驱动程序版本”  。
6.  对于“目标设备名称”  ，请选择配置用于测试和调试的计算机名。 在本练习中，我们使用名为 MyTestComputer 的计算机。
7.  选择“硬件 ID 驱动程序更新”  ，然后输入驱动程序的硬件 ID。 在本练习中，硬件 ID 为 Root\\KmdfHelloWorld。 单击“确定”  。

    ![“kmdfhelloworld 属性页”窗口的屏幕截图，显示选择了“部署驱动程序安装” ](images/vs2015-kmdf-hello-world-property-pages.png)

    >[!NOTE]
    > 在本练习中，硬件 ID 不标识真实的硬件。 它标识了虚构设备，该设备位于[设备树](device-nodes-and-device-stacks.md)中，作为根节点的子节点。 对于真实的硬件，不要选择“硬件 ID 驱动程序更新”  ，而要选择“安装并验证”  。 你将在驱动程序的信息 (INF) 文件中看到硬件 ID。 在“解决方案资源管理器”  窗口中，转到“KmdfHelloWorld”&gt;“驱动程序文件”  ，然后双击 KmdfHelloWorld.inf。 硬件 ID 位于 \[Standard.NT$ARCH$\] 下。

    ```C++
    [Standard.NT$ARCH$]
    %KmdfHelloWorld.DeviceDesc%=KmdfHelloWorld_Device, Root\KmdfHelloWorld
    ```

8. 在“生成”  菜单上，选择“部署解决方案”  。 Visual Studio 会自动将安装和运行驱动程序所需的文件复制到目标计算机。 此操作可能会需要一两分钟的时间。

    部署驱动程序时，驱动程序文件将复制到测试计算机上的 %Systemdrive%\drivertest\drivers 文件夹。 如果部署期间发生错误，可以查看这些文件是否已复制到测试计算机。 请确认 .inf、.cat、测试证书和 .sys 文件以及其他任何必要的文件均位于 %systemdrive%\drivertest\drivers 文件夹中。

    有关部署驱动程序的详细信息，请参阅[将驱动程序部署到测试计算机](../develop/deploying-a-driver-to-a-test-computer.md)。

## <a name="install-the-driver"></a>安装驱动程序

将 Hello World 驱动程序部署到目标计算机后，即可安装该驱动程序。 如果你之前使用“自动”  选项通过 Visual Studio 预配了目标计算机，则在预配过程中，Visual Studio 会将目标计算机设置为运行测试签名驱动程序。 现在，你只需使用 DevCon 工具安装驱动程序即可。

1. 在主计算机上，导航到 WDK 安装中的“Tools”文件夹，然后找到 DevCon 工具。 例如，在以下文件夹中查看：

    *C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe*

    将 DevCon 工具复制到远程计算机。

2. 在目标计算机上，导航到包含驱动程序文件的文件夹，然后运行 DevCon 工具，以安装驱动程序。 
    1. 以下是将用于安装驱动程序的 devcon 工具的常规语法：

        devcon install \<INF 文件\> \<硬件 ID\> 

        安装此驱动程序所需的 INF 文件是 KmdfHelloWorld.inf。 INF 文件包含用于安装驱动程序二进制文件 *KmdfHelloWorld.sys* 的硬件 ID。 回想一下，位于 INF 文件中的硬件 ID 是 **Root\\KmdfHelloWorld**。
    2. 以管理员身份打开命令提示符窗口。 导航到内置驱动程序 .sys 文件所在的文件夹，然后输入以下命令：

        **devcon install kmdfhelloworld.inf root\\kmdfhelloworld**

        如果收到一条关于 devcon  未被识别的错误消息，请尝试添加 devcon  工具的路径。 例如，如果已将其复制到目标计算机上称为 *C:\\Tools* 的文件夹，则尝试使用以下命令：

        **c:\\tools\\devcon install kmdfhelloworld.inf root\kmdfhelloworld**

        此时将显示一个对话框，指示测试驱动程序是未签名驱动程序。 单击“仍然安装此驱动程序”  以继续。

        ![驱动程序安装警告的屏幕截图](../debugger/images/debuglab-image-install-security-warning.png)

## <a name="debug-the-driver"></a>调试驱动程序

现在，你已在目标计算机上安装了 KmdfHelloWorld 驱动程序，将从主计算机远程连接调试程序。

1. 在主计算机上，以管理员身份打开命令提示符窗口。 转到 WinDbg.exe 目录。 我们将使用安装 Windows 工具包过程中安装的 Windows 驱动程序工具包 (WDK) 中的 x64 版本 WinDbg.exe。 下面是 WinDbg.exe 的默认路径：

    *C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64*

2. 使用以下命令启动 WinDbg 以连接到目标计算机上的内核调试会话。 端口和密钥的值应该与你预配目标计算机所使用的值相同。 我们将使用 **50000** 作为端口，使用 **1.2.3.4** 作为密钥。我们在部署步骤中使用过这些值。 *K* 标志指示这是内核调试会话。

    **WinDbg -k net:port=50000,key=1.2.3.4**

3.  在“调试”  菜单上，选择“中断”  。 主计算机上的调试程序将中断目标计算机。 在“调试程序命令”  窗口中，你可以看到内核调试命令提示符：**kd\>** 。

4. 此时，可以试验调试程序，方法是在 **kd&gt;** 提示符处输入命令。 例如，可以尝试使用以下命令：

    -   [lm](https://go.microsoft.com/fwlink/p?linkid=399236)
    -   [.sympath](https://go.microsoft.com/fwlink/p?linkid=399238)
    -   [.reload](https://go.microsoft.com/fwlink/p?linkid=399239)
    -   [x KmdfHelloWorld!\*](https://go.microsoft.com/fwlink/p?linkid=399240)

5. 若要让目标计算机再次运行，请从“调试”  菜单中选择“执行”  ，或者按“g”，然后按“Enter”。
6. 若要停止调试会话，请从“调试”  菜单中选择“分离调试程序”  。

    > [!IMPORTANT]
    > 请确保在退出调试程序之前使用“执行”命令让目标计算机再次运行，否则目标计算机将仍然对你的鼠标和键盘输入无响应，因为它仍在与调试程序通话。

有关驱动程序调试过程的详细分步演练，请参阅[调试通用驱动程序 - 分步实验室（回显内核模式）](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。

有关远程调试的详细信息，请参阅[使用 WinDbg 远程调试](../debugger/remote-debugging-using-windbg.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[开发、测试以及部署驱动程序](https://go.microsoft.com/fwlink/p?linkid=399234)

[Windows 调试工具](https://go.microsoft.com/fwlink/p?linkid=223405)

[调试通用驱动程序 - 分步实验室（回显内核模式）](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)

[编写你的第一个驱动程序](writing-your-first-driver.md)
