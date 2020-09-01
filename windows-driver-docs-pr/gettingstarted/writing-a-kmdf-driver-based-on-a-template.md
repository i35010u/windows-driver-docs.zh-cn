---
title: 基于模板编写通用 Windows 驱动程序 (KMDF)
description: 本主题介绍了如何使用内核模式驱动程序框架 (KMDF) 编写通用 Windows 驱动程序。 首先使用 Microsoft Visual Studio 模板，然后在单独的计算机上部署和安装驱动程序。
ms.assetid: 1E15A136-94BB-46C1-A438-9562C6BDCE7E
keywords:
- 编写 KMDF 驱动程序
ms.date: 04/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8b6b239e2e4f976bf62efe9536690df5d3889b2b
ms.sourcegitcommit: 9e5a99dc75dfee3caa9a242adc0ed22ae4df9f29
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89043153"
---
# <a name="write-a-universal-windows-driver-kmdf-based-on-a-template"></a>基于模板编写通用 Windows 驱动程序 (KMDF)

本主题介绍了如何使用内核模式驱动程序框架 (KMDF) 编写[通用 Windows 驱动程序](https://docs.microsoft.com/windows-hardware/drivers)。 首先使用 Microsoft Visual Studio 模板，然后在单独的计算机上部署和安装驱动程序。

若要开始操作，请确保已安装最新版本的 [Microsoft Visual Studio]https://visualstudio.microsoft.com/vs/) 和 [Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。

安装 WDK 时，需要包括 [Windows 调试工具](https://docs.microsoft.com/windows-hardware/drivers/debugger/)。

## <a name="create-and-build-a-driver-package"></a>创建和生成驱动程序包

1. 打开 Microsoft Visual Studio。 在“文件”菜单上，选择“新建”&gt;“项目”。 这将打开“新建项目”对话框，如下所示。
2. 在“新建项目”对话框中，选择 **WDF**。
3. 在中间窗格中，选择“内核模式驱动程序(KMDF)”。
4. 在“名称”字段中，输入“KmdfDriver”作为项目名称。

    > [!NOTE]
    > 在创建新的 KMDF 或 UMDF 驱动程序时，必须选择一个不多于 32 个字符的驱动程序名称。 此长度限制在 wdfglobals.h 中定义。  

5. 在“位置”字段中，输入要在其中创建新项目的目录。
6. 选中“创建解决方案的目录”。 选择“确定”。

    ![“新建项目”对话框的屏幕截图，显示选中的 WDF 和内核模式驱动程序](images/vs2015-kmdf-new-project.png)

    Visual Studio 将创建一个项目和一个解决方案。 你可以在“解决方案资源管理器”窗口中看到它们，如下所示。 （如果未显示“解决方案资源管理器”窗口，请从“视图” 菜单中选择“解决方案资源管理器”。）该解决方案有一个名为 KmdfDriver 的驱动程序项目。 若要查看驱动程序源代码，请打开**源文件**下的任何文件。 可以先从 Driver.c 和 Device.c 开始。

    ![解决方案资源管理器的屏幕截图，其中显示驱动程序项目和程序包项目中的文件](images/vs2015-kmdf-solution-explorer.png)

7. 在“解决方案资源管理器”窗口中，选择并按住（或右键单击）“解决方案‘KmdfDriver’(1 个项目)”，然后选择“配置管理器”  。 为驱动程序项目和程序包项目选择配置和平台。 在本练习中，我们选择“调试”和“x64”。

8. 若要生成驱动程序并创建驱动程序包，请从“生成”菜单中选择“生成解决方案”。 Visual Studio 在“输出”窗口中显示生成进度。 （如果“输出”窗口不可见，请从“视图”菜单中选择“输出”。）

    确认解决方案成功生成后，可以关闭 Visual Studio。

9. 若要查看生成的驱动程序，请在“文件资源管理器”中，依次转到 **KmdfDriver** 文件夹和 **x64\\Debug\\KmdfDriver**。 该文件夹包括：

    * KmdfDriver.sys - 内核模式驱动程序文件
    * KmdfDriver.inf -- 在安装驱动程序时 Windows 使用的信息文件

## <a name="deploy-the-driver"></a>部署驱动程序

通常，在测试和调试驱动程序时，调试程序和驱动程序会在不同的计算机上运行。 运行调试程序的计算机称为“主计算机”，运行驱动程序的计算机称为“目标计算机”。 目标计算机也称为“测试计算机”。 有关调试驱动程序的详细信息，请参阅 [Windows 调试工具](https://docs.microsoft.com/windows-hardware/drivers/debugger/)。

到目前为止，你已在主计算机上使用 Visual Studio 生成了驱动程序。 现在，需要配置目标计算机。

1. 按照[预配计算机以便进行驱动程序部署和测试 (WDK 10)](provision-a-target-computer-wdk-8-1.md) 中的说明进行操作。

    > [!TIP]
    > 按照步骤使用网络电缆自动预配目标计算机时，请记下端口和密钥。 以后，你将在调试步骤中使用它们。 在此示例中，我们将使用 **50000** 作为端口，使用 **1.2.3.4** 作为密钥。
    >
    > 在实际的驱动程序调试方案中，我们建议使用 KDNET 生成的密钥。 有关如何使用 KDNET 生成一个随机密钥的详细信息，请参阅[调试驱动程序 - 分步实验室（Sysvad 内核模式）](../debugger/debug-universal-drivers--kernel-mode-.md)主题。

2. 在主计算机上，在 Visual Studio 中打开你的解决方案。 你可以在 KmdfDriver 文件夹中双击解决方案文件 KmdfDriver.sln。
3. 在“解决方案资源管理器”窗口中，选择并按住（或右键单击）KmdfDriver 项目，然后选择“属性”  。
4. 在“KmdfDriver 包属性页”窗口的左侧窗格中，转到“配置属性”&gt;“驱动程序安装”&gt;“部署”。
5. 选中“部署前删除以前的驱动程序版本”。
6. 对于**远程计算机名**，请选择配置用于测试和调试的计算机名。 在本练习中，我们使用名为 MyTestComputer 的计算机。
7. 选择“硬件 ID 驱动程序更新”，然后输入驱动程序的硬件 ID。 在本练习中，硬件 ID 为“Root\\KmdfDriver”。 选择“确定”。

    ![“kmdfdriver 包属性页”窗口的屏幕截图，其中显示选择了“部署驱动程序安装”](images/vs2015-kmdfdriver-property-pages.png)

    > [!NOTE]
    > 在本练习中，硬件 ID 不标识真实的硬件。 它标识了虚构设备，该设备位于[设备树](https://go.microsoft.com/fwlink/p?linkid=399236)中，作为根节点的子节点。 对于真实的硬件，不要选择“硬件 ID 驱动程序更新”，而要选择“安装并验证”。 你将在驱动程序的信息 (INF) 文件中看到硬件 ID。 在“解决方案资源管理器”窗口中，转到“KmdfDriver”&gt;“驱动程序文件”，然后双击 KmdfDriver.inf。 硬件 ID 位于 \[Standard.NT$ARCH$\] 下。

    ```C++
    [Standard.NT$ARCH$]
    %KmdfDriver.DeviceDesc%=KmdfDriver_Device, Root\KmdfDriver
    ```

8. 在“生成”菜单上，选择“部署解决方案”。 Visual Studio 会自动将安装和运行驱动程序所需的文件复制到目标计算机。 此操作可能会需要一两分钟的时间。

    部署驱动程序时，驱动程序文件将复制到测试计算机上的 %Systemdrive%\drivertest\drivers 文件夹。 如果部署期间发生错误，可以查看这些文件是否已复制到测试计算机。 请确认 .inf、.cat、测试证书和 .sys 文件以及其他任何必要的文件均位于 %systemdrive%\drivertest\drivers 文件夹中。

    有关部署驱动程序的详细信息，请参阅[将驱动程序部署到测试计算机](../develop/deploying-a-driver-to-a-test-computer.md)。

## <a name="install-the-driver"></a>安装驱动程序

将 KMDF 驱动程序部署到目标计算机后，现在你将安装该驱动程序。 如果你之前使用“自动”选项通过 Visual Studio 预配了目标计算机，则在预配过程中，Visual Studio 会将目标计算机设置为运行测试签名驱动程序。 现在，你只需使用 DevCon 工具安装驱动程序即可。

1. 在主计算机上，导航到 WDK 安装中的“Tools”文件夹，然后找到 DevCon 工具。 例如，在以下文件夹中查看：

    *C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe*

    将 DevCon 工具复制到远程计算机。

2. 在目标计算机上，导航到包含驱动程序文件的文件夹，然后运行 DevCon 工具，以安装驱动程序。
    1. 以下是将用于安装驱动程序的 devcon 工具的常规语法：

        *devcon install \<INF file\> \<hardware ID\>*

        安装此驱动程序所需的 INF 文件是 KmdfDriver.inf。 INF 文件包含用于安装驱动程序二进制文件 *KmdfDriver.sys* 的硬件 ID。 回想一下，位于 INF 文件中的硬件 ID 是 **Root\\KmdfDriver**。
    2. 以管理员身份打开命令提示符窗口。 导航到你的驱动程序包文件夹，然后输入以下命令：

        **devcon install kmdfdriver.inf root\\kmdfdriver**

        如果你收到一条关于 devcon 未被识别的错误消息，请尝试添加 devcon 工具的路径。 例如，如果已将其复制到目标计算机上称为 *C:\\Tools* 的文件夹，则尝试使用以下命令：

        **c:\\tools\\devcon install kmdfdriver.inf root\kmdfdriver**

        此时将显示一个对话框，指示测试驱动程序是未签名驱动程序。 选择“仍然安装此驱动程序”以继续。

        ![驱动程序安装警告的屏幕截图](../debugger/images/debuglab-image-install-security-warning.png)

## <a name="debug-the-driver"></a>调试驱动程序

现在，你已在目标计算机上安装了 KMDF 驱动程序，你将从主计算机远程连接调试程序。

1. 在主计算机上，以管理员身份打开命令提示符窗口。 转到 WinDbg.exe 目录。 我们将使用安装 Windows 工具包过程中安装的 Windows 驱动程序工具包 (WDK) 中的 x64 版本 WinDbg.exe。 下面是 WinDbg.exe 的默认路径：

    *C:\\Program Files (x86)\\Windows Kits\\10\\Debuggers\\x64*

2. 使用以下命令启动 WinDbg 以连接到目标计算机上的内核调试会话。 端口和密钥的值应该与你预配目标计算机所使用的值相同。 我们将使用 **50000** 作为端口，使用 **1.2.3.4** 作为密钥。我们在部署步骤中使用过这些值。 *K* 标志指示这是内核调试会话。

    **WinDbg -k net:port=50000,key=1.2.3.4**

3. 在“调试”菜单上，选择“中断”。 主计算机上的调试程序将中断目标计算机。 在“调试程序命令”窗口中，你可以看到内核调试命令提示符：**kd\>** 。

4. 此时，可以试验调试程序，方法是在 **kd&gt;** 提示符处输入命令。 例如，可以尝试使用以下命令：

    * [lm](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)
    * [.sympath](https://docs.microsoft.com/windows-hardware/drivers/debugger/-sympath--set-symbol-path-)
    * [.reload](https://docs.microsoft.com/windows-hardware/drivers/debugger/-reload--reload-module-)
    * [x KmdfHelloWorld!\*](https://docs.microsoft.com/windows-hardware/drivers/debugger/x--examine-symbols-)

5. 若要让目标计算机再次运行，请从“调试”菜单中选择“执行”，或者按“g”，然后按“Enter”。
6. 若要停止调试会话，请从“调试”菜单中选择“分离调试程序”。

    > [!IMPORTANT]
    > 请确保在退出调试程序之前使用“执行”命令让目标计算机再次运行，否则目标计算机将仍然对你的鼠标和键盘输入无响应，因为它仍在与调试程序通话。

有关驱动程序调试过程的详细分步演练，请参阅[调试通用驱动程序 - 分步实验室（回显内核模式）](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。

有关远程调试的详细信息，请参阅[使用 WinDbg 远程调试](../debugger/remote-debugging-using-windbg.md)。

## <a name="using-the-driver-module-framework-dmf"></a>使用驱动程序模块框架 (DMF)

[驱动程序模块 Framework (DMF)](https://github.com/Microsoft/DMF) 是 WDF 的一个扩展，可为 WDF 驱动程序开发人员提供额外的功能。 它可以帮助开发人员更快、更好地编写任何类型的 WDF 驱动程序。

作为一个框架，DMF 可用于创建称作“DMF 模块”的 WDF 对象。 可以在不同的驱动程序之间共享这些 DMF 模块的代码。 此外，DMF 捆绑了为我们为驱动程序开发的 DMF 模块库，可为其他驱动程序开发人员提供价值。

DMF 不会取代 WDF。 DMF 是与 WDF 搭配使用的另一个框架。 利用 DMF 的开发人员仍需使用 WDF 及其所有基元来编写设备驱动程序。

有关详细信息，请参阅[驱动程序模块框架 (DMF)](https://github.com/Microsoft/DMF)。

## <a name="related-topics"></a>相关主题

[开发、测试以及部署驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/)

[Windows 调试工具](https://docs.microsoft.com/windows-hardware/drivers/debugger/)

[调试通用驱动程序 - 分步实验室（回显内核模式）](../debugger/debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)

[编写你的第一个驱动程序](writing-your-first-driver.md)
