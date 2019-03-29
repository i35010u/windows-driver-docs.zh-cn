---
title: 调试驱动程序-分步实验室 （Sysvad 内核模式）
description: 此实验室提供了演示如何调试 Sysvad 音频的内核模式设备驱动程序的实际练习。
ms.assetid: 4A31451C-FC7E-4C5F-B4EB-FBBAC8DADF9E
keywords:
- 调试实验室
- step-by-step
- SYSVAD
ms.date: 02/21/2019
ms.localizationpriority: medium
ms.openlocfilehash: f080677e88433499d3a8ee3840d3810e8aa476b6
ms.sourcegitcommit: a43a696c5b4d2f08ee77d507631b41ecfdea6742
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/22/2019
ms.locfileid: "56666735"
---
# <a name="span-iddebuggerdebuguniversaldriverskernel-modespandebug-drivers---step-by-step-lab-sysvad-kernel-mode"></a><span id="debugger.debug_universal_drivers__kernel-mode_"></span>调试驱动程序的执行步骤的实验室 （Sysvad 内核模式）

此实验室提供了演示如何调试 Sysvad 音频的内核模式设备驱动程序的实际练习。

Microsoft Windows 调试器 (WinDbg) 是一个功能强大的基于 Windows 的调试工具，可用于执行用户模式和内核模式调试。 WinDbg 提供了源代码级别调试的 Windows 内核、 内核模式驱动程序和系统服务，以及用户模式应用程序和驱动程序。

WinDbg 可以单步执行源代码，设置断点，查看变量 （包括 c + + 对象）、 堆栈跟踪和内存。 其调试器命令窗口中，用户可以发出各种命令。

## <a name="span-idlabsetupspanlab-setup"></a><span id="lab_setup"></span>实验室设置

您将需要能够完成该实验的以下硬件：

-   便携式计算机或台式计算机 （主机） 运行 Windows 10
-   便携式计算机或台式计算机 （目标） 运行 Windows 10
-   网络中心/路由器和网络电缆连接两台 Pc
-   访问 internet 以下载符号文件

你将需要以下软件才能将无法完成该实验。

-   Microsoft Visual Studio 2017
-   适用于 Windows 10 的 Windows 软件开发工具包 (SDK)
-   适用于 Windows 10 的 Windows 驱动程序工具包 (WDK)
-   该示例 Sysvad 音频驱动程序适用于 Windows 10

有关下载和安装 WDK 的信息，请参阅[下载 Windows Driver Kit (WDK)](https://developer.microsoft.com/windows/hardware/windows-driver-kit)。

## <a name="span-idsysvaddebuggingwalkthroughoverviewspansysvad-debugging-walkthrough"></a><span id="sysvad_debugging_walkthrough_overview"></span>Sysvad 调试演练


此实验室将引导你完成调试的内核模式驱动程序的过程。 练习使用 Syvad 虚拟音频驱动程序示例。 因为 Syvad 音频驱动程序不会与实际的音频硬件进行交互，可以在大多数设备上使用它。 实验室涵盖以下任务：

-   [第 1 部分：连接到内核模式 WinDbg 会话](#connectto)
-   [第 2 部分： 内核模式调试命令和技术](#kernelmodedebuggingcommandsandtechniques)
-   [第 3 部分：下载并构建 Sysvad 音频驱动程序](#download)
-   [第 4 部分：在目标系统上安装 Sysvad 音频驱动程序](#install)
-   [第 5 部分：使用 WinDbg 显示有关驱动程序的信息](#usewindbgtodisplayinformation)
-   [第 6 部分：显示插设备树信息](#displayingtheplugandplaydevicetree)
-   [第 7 部分：使用断点和源代码](#workingwithbreakpoints)
-   [第 8 部分：查看变量](#lookingatvariables)
-   [第 9 部分：查看调用堆栈](#viewingcallstacks)
-   [第 10 部分：显示进程和线程](#displayingprocessesandthreads)
-   [第 11 节：IRQL，寄存器和反汇编](#irqlregistersmemory)
-   [第 12 节：使用内存](#workingwithmemory)
-   [第 13 节：结束 WinDbg 会话](#endingthesession)
-   [第 14 节：Windows 调试资源](#windowsdebuggingresources)

## <a name="span-idechodriverlabspanecho-driver-lab"></a><span id="echo_driver_lab"></span>Echo 驱动程序实验室


Echo 驱动程序是一个更简单的驱动程序然后 Sysvad 音频驱动程序。 如果您不熟悉 WinDbg，您可能想要考虑首先完成[调试通用驱动程序的分步实验室 （Echo 内核模式）](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。 此实验室重复使用从该实验室的安装说明操作，因此如果您已完成该实验，则可以跳过部分 1 和 2 此处。

## <a name="span-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span>第 1 部分：连接到内核模式 WinDbg 会话


*在第 1 部分，将配置网络在主机和目标系统上进行调试。*

此实验室中的 Pc 需要将配置为使用以太网网络连接进行内核调试。

此实验使用两台计算机。 运行 WinDbg*主机*上运行的系统和 Sysvad 驱动程序*目标*系统。

 使用网络中心/路由器和网络电缆连接两台 Pc。

![与双向箭头连接的两台 pc](images/debuglab-image-targethostdrawing1.png)

若要使用内核模式应用程序并使用 WinDbg，我们建议通过以太网传输使用 KDNET。 有关如何使用以太网传输协议的信息，请参阅[开始使用 WinDbg （内核模式）](getting-started-with-windbg--kernel-mode-.md)。 有关设置目标计算机的详细信息，请参阅[手动驱动程序部署准备一台计算机](https://msdn.microsoft.com/windows-drivers/develop/preparing_a_computer_for_manual_driver_deployment)并[设置向上 KDNET 网络内核调试自动](setting-up-a-network-debugging-connection-automatically.md)。

### <a name="span-idconfigurekernelmodedebuggingusingethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="configure__kernel_mode_debugging_using_ethernet"></span>配置内核模式 – 调试使用以太网

若要启用内核模式下在目标系统上进行调试，请执行以下步骤。

**&lt;在主机系统**

1. 打开命令提示符上的主机系统和类型**ipconfig /all**以确定其 IP 地址。

```console
C:\>ipconfig /all
Windows IP Configuration

 Host Name . . . . . . . . . . . . : TARGETPC
...

Ethernet adapter Ethernet:
   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::c8b6:db13:d1e8:b13b3
   Autoconfiguration IPv4 Address. . : 169.182.1.1
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . :
```

2. 记录主机系统的 IP 地址： \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

3. 记录主机系统的主机名称： \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**-&gt; 在目标系统上**

4. 打开在目标系统上的命令提示符，并使用**ping**命令来确认这两个系统之间的网络连接。 而不是示例输出所示的 169.182.1.1 使用主机系统所记录的实际 IP 地址。

```console
C:\> ping 169.182.1.1

Pinging 169.182.1.1 with 32 bytes of data:
Reply from 169.182.1.1: bytes=32 time=1ms TTL=255
Reply from 169.182.1.1: bytes=32 time<1ms TTL=255
Reply from 169.182.1.1: bytes=32 time<1ms TTL=255
Reply from 169.182.1.1: bytes=32 time<1ms TTL=255

Ping statistics for 169.182.1.1:
    Packets: Sent = 4, Received = 4, Lost = 0 (0% loss),
Approximate round trip times in milli-seconds:
    Minimum = 0ms, Maximum = 1ms, Average = 0ms
```

若要使用 KDNET 实用工具启用内核模式调试在目标系统上，执行以下步骤。

1. 在主机系统上，找到 WDK KDNET 目录。 默认情况下它位于此处。

   C:\Program Files (x86)\Windows Kits\10\Debuggers\x64

> [!NOTE]
> 此实验室假定这两台 Pc 运行 Windowson 的 64 位版本的目标和主机。 如果这不是这样，最好的方法是运行在目标主机上运行工具的同一"位数"。 例如，如果目标是正在运行 32 位 Windows，在主机上运行 32 版本的调试器。 有关详细信息，请参阅[选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
> 

2. 查找这两个文件并将它们复制到网络共享或拇指驱动器，以便它们可在目标计算机上。

    kdnet.exe

    VerifiedNICList.xml


3. 在目标计算机上，以管理员身份打开命令提示符窗口。 输入以下命令来验证目标 PC 上的 NIC 是支持。

```console
C:\KDNET>kdnet

Network debugging is supported on the following NICs:
busparams=0.25.0, Intel(R) 82579LM Gigabit Network Connection, KDNET is running on this NIC.kdnet.exe
```

4. 键入以下命令以设置主机系统的 IP 地址。 而不是示例输出所示的 169.182.1.1 使用主机系统所记录的实际 IP 地址。 选择您使用，如 50010 每个目标/主机对一个唯一的端口地址。

```console
C:\>kdnet 169.182.1.1 50010

Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。
>

5. 键入以下命令以确认正确设置 dbgsettings。

```console
C:\> bcdedit /dbgsettings
busparams               0.25.0
key                     2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
debugtype               NET
hostip                  169.182.1.1
port                    50010
dhcp                    Yes
The operation completed successfully.
```

自动复制到文本文件，以避免无需键入其宿主 PC 上生成的唯一键。 将文本文件具有键复制到主机系统。

**请注意**  
**防火墙和调试器**

如果从防火墙，看到一个弹出消息，并且你想要使用调试器，检查**所有这三个**的框。

![windows 安全警报的 windows 防火墙已阻止此应用的某些功能](images/debuglab-image-firewall-dialog-box.png)
 

**&lt;在主机系统**

1. 在主计算机上，以管理员身份打开命令提示符窗口。 转到 WinDbg.exe 目录。 我们将使用安装 Windows 工具包过程中安装的 Windows 驱动程序工具包 (WDK) 中 x64 版本的 WinDbg.exe。

```console
C:\> Cd C:\Program Files (x86)\Windows Kits\10\Debuggers\x64 
```

2. 使用远程用户调试使用以下命令启动 WinDbg。 密钥和端口的值与匹配您之前在目标系统上使用 BCDEdit 设置。

```console
C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

**-&gt;在目标系统上**

重新启动目标系统。

**&lt;在主机系统**

在一分钟或两个，应在主机系统上显示调试输出。

![windows 调试器实时内核连接进行连接时显示命令窗口输出](images/debuglab-image-winddbg-hh.png)

调试器命令窗口是在 WinDbg 中主要的调试信息窗口。 您可以输入的调试器命令，在此窗口中查看命令输出。

调试器命令窗口拆分为两个窗格。 在窗口底部的小窗格 （命令项窗格） 中键入命令，并在更大窗口的顶部窗格中查看命令输出。

在命令项窗格中，使用向上箭头和向下箭头键可以滚动浏览命令历史记录。 命令出现时，你可以对其进行编辑，或按**ENTER**运行命令。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="kernelmodedebuggingcommandsandtechniques"></span>第 2 部分： 内核模式调试命令和技术


*在第 2 部分，您将使用调试命令来显示有关目标系统的信息。*

**&lt;在主机系统**

**让调试器标记语言 (DML) 使用.prefer\_dml**

一些调试命令的显示文本使用调试器标记语言，可以单击快速收集的详细信息。

1. 在 WinDBg 中使用 Ctrl + Break (Scroll Lock) 分解为目标系统上运行的代码。 可能需要一些时间才能在目标系统进行响应。
2. 键入以下命令以启用 DML 调试器命令窗口中。

```dbgcmd
0: kd> .prefer_dml 1
DML versions of commands on by default
```

**使用.hh * 若要获取帮助**

可以参考命令帮助使用访问 **.hh *** 命令。

3. 键入以下命令以查看命令的参考帮助 **.prefer\_dml**。
   ```dbgcmd
   0: kd> .hh .prefer_dml
   ```

调试器帮助文件将显示的帮助 **.prefer\_dml**命令。

![调试器帮助应用程序显示帮助.prefer\-dml 命令](images/debuglab-image-prefer-dml-help.png)

**显示目标系统上的 Windows 版本**

5. 通过键入目标系统上显示详细的版本信息[ **vertarget （显示目标计算机版本）** ](vertarget--show-target-computer-version-.md) WinDbg 窗口命令。

```dbgcmd
0: kd> vertarget
Windows 10 Kernel Version 9926 MP (4 procs) Free x64
Product: WinNt, suite: TerminalServer SingleUserTS
Built by: 9926.0.amd64fre.fbl_awesome1501.150119-1648
Machine Name: ""
Kernel base = 0xfffff801`8d283000 PsLoadedModuleList = 0xfffff801`8d58aef0
Debug session time: Fri Feb 20 10:15:17.807 2015 (UTC - 8:00)
System Uptime: 0 days 01:31:58.931
```

**列出已加载的模块**

6. 你可以验证你正在与正确的内核模式进程通过显示已加载的模块，通过键入[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md) WinDbg 窗口命令。

```dbgcmd
0: Kd> lm
start             end                 module name
fffff801`09200000 fffff801`0925f000   volmgrx    (no symbols)           
fffff801`09261000 fffff801`092de000   mcupdate_GenuineIntel   (no symbols)           
fffff801`092de000 fffff801`092ec000   werkernel   (export symbols)       werkernel.sys
fffff801`092ec000 fffff801`0934d000   CLFS       (export symbols)       CLFS.SYS
fffff801`0934d000 fffff801`0936f000   tm         (export symbols)       tm.sys
fffff801`0936f000 fffff801`09384000   PSHED      (export symbols)       PSHED.dll
fffff801`09384000 fffff801`0938e000   BOOTVID    (export symbols)       BOOTVID.dll
fffff801`0938e000 fffff801`093f7000   spaceport   (no symbols)           
fffff801`09400000 fffff801`094cf000   Wdf01000   (no symbols)           
fffff801`094d9000 fffff801`09561000   CI         (export symbols)       CI.dll
...
```

**请注意**  已省略的输出指示"... "在此实验中。

 

因为我们尚未设置符号路径和已加载的符号，有限的信息可在调试器中。

## <a name="span-iddownloadspansection-3-download-and-build-the-sysvad-audio-driver"></a><span id="download"></span>第 3 部分：下载并构建 Sysvad 音频驱动程序


*在第 3 部分，将下载并生成 Sysvad 音频驱动程序。*

通常情况下，您应该使用与你自己的驱动程序代码使用 WinDbg 时。 若要熟悉调试音频驱动程序，请使用 Sysvad 虚拟音频示例驱动程序。 此示例用于说明如何可以单一单步执行本机内核模式代码。 这种技术都是用于调试复杂的内核模式代码问题非常有用。

若要下载并生成 Sysvad 示例音频驱动程序时，执行以下步骤。

1.  **下载并从 GitHub 提取 Sysvad 音频示例**

    您可以使用浏览器查看 Sysvad 示例和此处 Readme.md 文件：

    [https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    ![显示常规文件夹和下载 zip 按钮的 github 存储库](images/sysvad-lab-github.png)

    此实验中，演示如何下载一个 zip 文件中的通用驱动程序示例。

    a. Master.zip 文件下载到本地硬盘。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b. 右键单击*Windows 驱动程序示例 master.zip*，然后选择**全部提取**。 指定新文件夹，或浏览到一个现有将存储提取的文件。 例如，可以指定*c:\\WDK\_示例\\*作为文件提取到其中的新文件夹。

    c. 提取文件后，导航到以下子文件夹。

    *C:\\WDK\_示例\\Sysvad*

2.  **在 Visual Studio 中打开驱动程序解决方案**

    在 Visual Studio 中，单击**文件** &gt; **打开** &gt; **项目/解决方案...** 并导航到包含所提取的文件的文件夹 (例如， *c:\\WDK\_示例\\Sysvad*)。 双击*Syvad*解决方案文件。

    在 Visual Studio 中找到解决方案资源管理器。 (如果尚未打开，请将此选择**解决方案资源管理器**从**视图**菜单。)在解决方案资源管理器，可以看到有许多项目和中包含的内容的示例更改不时的一种解决方案。 
        
    ![visual studio 中的使用 device.c 文件加载从 sysvad 项目](images/sysvad-lab-visual-studio-solution.png)

3.  **设置示例的配置和平台**

    在解决方案资源管理器中右键单击**sysvad （7 项目） 的解决方案**，然后选择**Configuration Manager**。 请确保配置和平台设置是相同的四个项目。 默认情况下的配置设置为"Win10 Debug"，并将所有项目的平台设置为"Win64"。 如果你进行任何配置和/或平台更改为一个项目，必须进行的剩余三个项目相同的更改。

    **请注意**  此实验室假定正在使用 64 位 Windows。 如果使用的 32 位 Windows，构建适用于 32 位驱动程序。

     

4.  **检查驱动程序签名**

    找到 TabletAudioSample。 打开 Sysvad 驱动程序的属性页，请确保**驱动程序签名** &gt; **登录模式**设置为*测试登录*。

5.  **使用 Visual Studio 生成示例**

    在 Visual Studio 中，单击**构建** &gt; **生成解决方案**。

    生成 windows 应显示一条指示成功的所有六个项目生成消息。

6.  **找到的内置驱动程序文件**

    在文件资源管理器，导航到包含示例提取的文件的文件夹。 例如，你可以导航到*c:\\WDK\_示例\\Sysvad*，如果这是你在前面指定的文件夹。 在该文件夹中，已编译的驱动程序文件的位置而异的配置和平台设置中选择**Configuration Manager**。 例如，如果保留默认设置保持不变，然后将已编译的驱动程序文件将保存到名为的文件夹 *\\x64\\调试*为 64 位调试版本。

    导航到包含 TabletAudioSample 驱动程序的生成的文件的文件夹：

    *C:\\WDK\_示例\\Sysvad\\TabletAudioSample\\x64\\调试*。 该文件夹将包含 TabletAudioSample。SYS 驱动程序、 符号 pdp 文件和 inf 文件。 您还需要找到 SwapAPO 和 KeywordDetectorContosoAdapter dll 和符号文件。

    若要安装该驱动程序，您将需要以下文件。

    |                                   |                                                                                   |
    |-----------------------------------|-----------------------------------------------------------------------------------|
    | TabletAudioSample.sys             | 驱动程序文件中。                                                                  |
    | TabletAudioSample.pdb             | 驱动程序的符号文件。                                                           |
    | tabletaudiosample.inf             | 一个包含安装驱动程序所需信息的信息 (INF) 文件。 |
    | KeywordDetectorContosoAdapter.dl  | 示例关键字检测程序。                                                        |
    | KeywordDetectorContosoAdapter.pdb | 示例关键字检测器符号文件。                                          |
    | lSwapAPO.dll                      | UI 来管理未一个示例驱动程序扩展。                                |
    | lSwapAPO.pdb                      | APO UI 符号文件。                                                           |
    | TabletAudioSample.cer             | TabletAudioSample 证书文件。                                           |

     

7.  找到 USB 拇指驱动器或网络共享设置为将内置驱动程序文件复制到目标系统主机中。

在下一步部分中，会将代码复制到目标系统中，并安装和测试驱动程序。

## <a name="span-idinstallspansection-4-install-the-sysvad-audio-driver-sample-on-the-target-system"></a><span id="install"></span>第 4 部分：在目标系统上安装 Sysvad 音频驱动程序示例


*在第 4 部分，您将使用 devcon 安装 Sysvad 音频驱动程序。*

**-&gt; 在目标系统上**

安装该驱动程序的计算机称为*目标计算机*或*测试计算机*。 通常情况下，这是在其开发和生成的驱动程序包的计算机不同的计算机。 开发和生成该驱动程序的计算机称为*主机计算机*。

将驱动程序包移动到目标计算机和安装该驱动程序的过程称为*部署*驱动程序。 你可以自动或手动部署示例 Sysvad 驱动程序。

手动部署驱动程序之前，必须通过启用测试签名来准备目标计算机。 此外需要在 WDK 安装中找到 DevCon 工具。 在此之后就可以在目标系统上运行内置的驱动程序示例。

若要在目标系统上安装该驱动程序，请执行以下步骤。

1.  **启用测试签名驱动程序**

    若要启用的功能运行测试签名驱动程序：

    1. 打开 Windows 设置。

    2. 在中**更新和安全**，选择**恢复**。

    3. 下**高级启动**，单击**立即重新启动**。

    4. PC 重新启动时，选择**疑难解答**。

    5. 然后选择**高级选项**，**启动设置**，然后单击**重启**。

    6. 通过按选择禁用强制驱动程序签名**F7**密钥。

    7. PC 将开始位置中的新值。

2.  **&lt;在主机系统**

    导航到 WDK 安装中的工具文件夹并找到 DevCon 工具。 例如，在以下文件夹中查看：

    *C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe*

3.  **-&gt; 在目标系统上**

    **安装驱动程序**

    以下说明介绍如何安装和测试的示例驱动程序。

    安装此驱动程序所需的 INF 文件*TabletAudioSample.inf*。 在目标计算机上，以管理员身份打开命令提示符窗口。 导航到驱动程序的包文件夹，右键单击 TabletAudioSample.inf 文件，并选择**安装**。

    此时将显示一个对话框，指示测试驱动程序是未签名驱动程序。 单击**仍然安装此驱动程序**以继续。

    ![windows 安全警告-windows 无法验证发布服务器](images/debuglab-image-install-security-warning.png)

    >[!TIP]
    > 如果已安装的任何问题，检查以下文件了解详细信息。
    `%windir%\inf\setupapi.dev.log`
    >
     
    有关详细说明，请参阅[配置一台计算机的驱动程序部署、 测试和调试](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

    INF 文件包含用于安装的硬件 ID *tabletaudiosample.sys*。 有关 Syvad 示例中，硬件 ID 是： `root\sysvad_TabletAudioSample`

    在目标计算机上，以管理员身份打开命令提示符窗口。 导航到驱动程序的包文件夹，并输入以下命令： `devcon status root\sysvad_TabletAudioSample`
       
    状态信息是 devcon 安装显示期间出现。


4.  **检查驱动程序在设备管理器**

    在目标计算机，在命令提示符窗口中，输入**devmgmt**打开设备管理器。 在设备管理器中，在视图菜单上选择**依类型排序设备**。

    在设备树中，找到*虚拟音频设备 (WDM) 的平板电脑示例*音频设备节点中。 这是在通常**声音、 视频和游戏控制器**节点。 确认已安装并处于活动状态。

    突出显示在设备管理器在 PC 上的实际硬件的驱动程序。 右键单击驱动程序，然后单击禁用对禁用的驱动程序。

    在设备管理器中确认该音频硬件的驱动程序，将显示向下箭头，指示已禁用。

    ![设备管理器树中突出显示的虚拟音频设备平板电脑示例](images/sysvad-lab-audio-device-manager.png)

    已成功安装后的示例驱动程序，现在，你准备好对其进行测试。

**测试 Sysvad 音频驱动程序**

1. 在目标计算机，在命令提示符窗口中，输入**devmgmt**打开设备管理器。 在设备管理器中，在**视图**菜单中，选择**依类型排序设备**。 在设备树中，找到*虚拟音频设备 (WDM) 的平板电脑示例*。

2. 打开控制面板并导航到**硬件和声音** &gt; **管理音频设备**。 在声音对话框中选择标记为的扬声器图标*虚拟音频设备 (WDM) 的平板电脑示例*，然后单击**设为默认值**，但不要单击**确定**。 这将保持声音对话框打开。
3. 查找 MP3 或目标计算机上的其他音频文件，然后双击以播放它。 然后在声音对话框，验证与关联的卷级别指示器中已有活动*虚拟音频设备 (WDM) 的平板电脑示例*驱动程序。

## <a name="span-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="usewindbgtodisplayinformation"></span>第 5 部分：使用 WinDbg 显示有关驱动程序的信息


*第 5 节中将设置符号路径，并使用内核调试器命令以显示有关 Sysvad 示例驱动程序信息。*

符号允许 WinDbg 以显示其他信息，如调试时非常有用的变量的名称。 WinDbg 使用 Microsoft Visual Studio 调试源代码级别调试符号格式。 从具有 PDB 符号文件的模块，它可以访问任何符号或变量。

若要加载的调试器，请执行以下步骤。

**&lt;在主机系统**

1.  如果关闭调试器时，打开管理员命令提示符窗口中再次使用以下命令。 将替换以前配置为密钥和端口。

    ```console
    C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
    ```

2.  使用 Ctrl + Break (Scroll Lock) 分解为目标系统上运行的代码。

**设置符号路径**

1.  若要向 Microsoft 符号服务器在 WinDbg 环境中设置符号路径，请使用 **.symfix**命令。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  若要添加你的本地符号位置使用本地符号，添加以下路径 using **.sympath +** ，然后 **.reload /f**。

    ```dbgcmd
    0: kd> .sympath+ C:\WDK_Samples\Sysvad
    0: kd> .reload /f
    ```

    **请注意**   **.reload**命令 **/f** force 选项将删除指定的模块的所有符号信息，然后重新加载符号。 在某些情况下，此命令还将重新加载或卸载该模块本身。

     

**请注意**  必须加载正确的符号使用 WinDbg 提供的高级的功能。 如果不具有正确配置的符号，将收到消息，指示的符号不可用时尝试使用依赖于符号的功能。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```

 

**请注意**  
**符号服务器**

有多种方法可用于使用符号。 在许多情况下，您可以从符号服务器，Microsoft 提供了在需要时访问符号配置 PC。 本演练假设将使用此方法。 如果你的环境中的符号不在不同的位置，来修改使用该位置的步骤。 有关其他信息，请参阅[符号存储区和符号服务器](symbol-stores-and-symbol-servers.md)。

 

**请注意**  
**了解源代码符号要求**

若要执行源代码调试，必须生成选中 （调试） 版本的二进制文件的位置。 编译器会创建符号文件 （.pdb 文件）。 这些符号文件将显示在调试器的二进制说明如何与源行相对应。 此外必须可以访问调试器本身的实际源文件。

符号文件不包含源代码的文本。 对于调试，最好是如果链接器不会优化你的代码。 源调试和本地变量的访问权限是更困难，并且有时几乎不可能，如果代码已经过优化。 如果您无法查看本地变量或源行，设置以下生成选项。

设置 COMPILE_DEBUG = 1

设置 ENABLE_OPTIMIZER = 0

 

1.  键入以下命令在命令区域中的调试器显示 Sysvad 驱动程序有关的信息。

    ```dbgcmd
    0: kd> lm m tabletaudiosample v
    Browse full module list
    start             end                 module name
    fffff801`14b40000 fffff801`14b86000   tabletaudiosample   (private pdb symbols)  C:\Debuggers\sym\TabletAudioSample.pdb\E992C4803EBE48C7B23DC1596495CE181\TabletAudioSample.pdb
        Loaded symbol image file: tabletaudiosample.sys
        Image path: \SystemRoot\system32\drivers\tabletaudiosample.sys
        Image name: tabletaudiosample.sys
        Browse all global symbols  functions  data
        Timestamp:        Thu Dec 10 12:20:26 2015 (5669DE8A)
        CheckSum:         0004891E
    ...  
    ```

    有关详细信息，请参阅[ **lm**](lm--list-loaded-modules-.md)。

2.  单击**浏览所有全局符号**中调试输出以显示有关以字母开头的项符号的信息的链接。
3.  由于启用了 DML，输出的某些元素是可单击的热链接。 单击*数据*中调试输出以显示有关以字母开头的项符号的信息的链接。

    ```dbgcmd
    0: kd> x /D /f tabletaudiosample!a*
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

    fffff806`9adb1000 tabletaudiosample!AddDevice (struct _DRIVER_OBJECT *, struct _DEVICE_OBJECT *)
    ```

    有关信息，请参阅[ **（检查符号） x**](x--examine-symbols-.md)。

4.  **！ Lmi**扩展显示有关模块的详细的信息。 类型 **！ lmi tabletaudiosample**。 输出应类似于如下所示的文本。

    ```dbgcmd
    0: kd> !lmi tabletaudiosample
    Loaded Module Info: [tabletaudiosample] 
             Module: tabletaudiosample
       Base Address: fffff8069ad90000
         Image Name: tabletaudiosample.sys
       Machine Type: 34404 (X64)
         Time Stamp: 58ebe848 Mon Apr 10 13:17:12 2017
               Size: 48000
           CheckSum: 42df7
    Characteristics: 22  
    Debug Data Dirs: Type  Size     VA  Pointer
                 CODEVIEW    a7,  e5f4,    d1f4 RSDS - GUID: {5395F0C5-AE50-4C56-AD31-DD5473BD318F}
                   Age: 1, Pdb: C:\Windows-driver-samples-master\audio\sysvad\TabletAudioSample\x64\Debug\TabletAudioSample.pdb
                       ??   250,  e69c,    d29c [Data not mapped]
         Image Type: MEMORY   - Image read successfully from loaded memory.
        Symbol Type: PDB      - Symbols loaded successfully from image header.
                     C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\sym\TabletAudioSample.pdb\5395F0C5AE504C56AD31DD5473BD318F1\TabletAudioSample.pdb
           Compiler: Resource - front end [0.0 bld 0] - back end [14.0 bld 24210]
        Load Report: private symbols & lines, not source indexed 
                     C:\Program Files (x86)\Windows Kits\10\Debuggers\x64\sym\TabletAudioSample.pdb\5395F0C5AE504C56AD31DD5473BD318F1\TabletAudioSample.pdb
    ```

5.  使用 **！ dh**扩展名，即可显示标头信息，如下所示。

    ```dbgcmd
    0: kd> !dh tabletaudiosample 

    File Type: EXECUTABLE IMAGE
    FILE HEADER VALUES
        8664 machine (X64)
           9 number of sections
    5669DE8A time date stamp Thu Dec 10 12:20:26 2015

           0 file pointer to symbol table
           0 number of symbols
          F0 size of optional header
          22 characteristics
                Executable
                App can handle >2gb addresses
    ...
    ```

## <a name="span-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="displayingtheplugandplaydevicetree"></span>第 6 部分：显示插设备树信息


*在第 6 节，将显示有关 Sysvad 示例设备驱动程序的信息和何处插设备树中。*

Plug and Play 设备树中的设备驱动程序有关的信息可用于故障排除。 例如，如果设备驱动程序不是驻留在设备树中，可以安装设备驱动程序出现问题。

有关设备节点调试扩展的详细信息，请参阅[ **！ devnode**](-devnode.md)。

**&lt;在主机系统**

1. 若要查看在插设备树中的所有设备节点，请输入 **！ devnode 0 1**命令。 此命令可能需要一分钟或两个运行。 此期间，"\*忙"将在 WinDbg 的状态区域中显示。

   ```dbgcmd
   0: kd> !devnode 0 1
   Dumping IopRootDeviceNode (= 0xffffe0005a3a8d30)
   DevNode 0xffffe0005a3a8d30 for PDO 0xffffe0005a3a9e50
     InstancePath is "HTREE\ROOT\0"
     State = DeviceNodeStarted (0x308)
     Previous State = DeviceNodeEnumerateCompletion (0x30d)
     DevNode 0xffffe0005a3a3d30 for PDO 0xffffe0005a3a4e50
       InstancePath is "ROOT\volmgr\0000"
       ServiceName is "volmgr"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeEnumerateCompletion (0x30d)
       DevNode 0xffffe0005a324560 for PDO 0xffffe0005bd95ca0…
   ...
   ```

2. 使用 Ctrl + F 来生成，以查找设备驱动程序，该名称在输出中搜索*sysvad*。

   ![查找对话框显示要搜索术语 sysvad](images/sysvad-lab-audio-find-dialog.png)

   设备节点条目的名称与`sysvad_TabletAudioSample`将会出现在 ！ Syvad devnode 输出。

   ```dbgcmd
     DevNode 0xffffe00086e68190 for PDO 0xffffe00089c575a0
       InstancePath is "ROOT\sysvad_TabletAudioSample\0000"
       ServiceName is "sysvad_tabletaudiosample"
       State = DeviceNodeStarted (0x308)
   ...
   ```

   请注意显示的 PDO 地址和 DevNode 地址。

3. 使用`!devnode 0 1 sysvad_TabletAudioSample`命令以显示与我们 Sysvad 设备驱动程序相关联的插信息。

   ```dbgcmd 
   0: kd> !devnode 0 1 sysvad_TabletAudioSample
   Dumping IopRootDeviceNode (= 0xffffe00082df8d30)
   DevNode 0xffffe00086e68190 for PDO 0xffffe00089c575a0
     InstancePath is "ROOT\sysvad_TabletAudioSample\0000"
     ServiceName is "sysvad_tabletaudiosample"
     State = DeviceNodeStarted (0x308)
     Previous State = DeviceNodeEnumerateCompletion (0x30d)
     DevNode 0xffffe000897fb650 for PDO 0xffffe00089927e30
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{64097438-cdc0-4007-a19e-62e789062e20}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00086d2f5f0 for PDO 0xffffe00089939ae0
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{78880f4e-9571-44a4-a9df-960bde446487}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00089759bb0 for PDO 0xffffe000875aa060
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{7cad07f2-d0a0-4b9b-8100-8dc735e9c447}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00087735010 for PDO 0xffffe000872068c0
       InstancePath is "SWD\MMDEVAPI\{0.0.0.00000000}.{fc38551b-e69f-4b86-9661-ae6da78bc3c6}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00088457670 for PDO 0xffffe0008562b830
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{0894b831-c9fe-4c56-86a6-092380fc5628}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe000893dbb70 for PDO 0xffffe00089d68060
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{15eb6b5c-aa54-47b8-959a-0cff2c1500db}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe00088e6f250 for PDO 0xffffe00089f6e990
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{778c07f0-af9f-43f2-8b8d-490024f87239}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
     DevNode 0xffffe000862eb4b0 for PDO 0xffffe000884443a0
       InstancePath is "SWD\MMDEVAPI\{0.0.1.00000000}.{e4b72c7c-be50-45df-94f5-0f2922b85983}"
       State = DeviceNodeStarted (0x308)
       Previous State = DeviceNodeStartPostWork (0x307)
   ```

4. 前一个命令中显示的输出包括与正在运行的驱动程序实例相关联的是 PDO，在此示例中它是*0xffffe00089c575a0*。 输入 **！ devobj**<em>&lt;PDO 地址&gt;</em>命令以显示与 Sysvad 设备驱动程序相关联的插信息。 使用 PDO 解决 **！ devnode**显示在您 PC 上，不是如下所示。

   ```dbgcmd 
   0: kd> !devobj 0xffffe00089c575a0
   Device object (ffffe00089c575a0) is for:
   0000004e \Driver\PnpManager DriverObject ffffe00082d47e60
   Current Irp 00000000 RefCount 65 Type 0000001d Flags 00001040
   SecurityDescriptor ffffc102b0f6d171 DevExt 00000000 DevObjExt ffffe00089c576f0 DevNode ffffe00086e68190 
   ExtensionFlags (0000000000)  
   Characteristics (0x00000180)  FILE_AUTOGENERATED_DEVICE_NAME, FILE_DEVICE_SECURE_OPEN
   AttachedDevice (Upper) ffffe00088386a50 \Driver\sysvad_tabletaudiosample
   Device queue is not busy.
   ```

5. 中显示的输出 **！ devobj**命令包含连接的设备的名称：\\驱动程序\\sysvad\_tabletaudiosample。 使用 **！ drvobj**命令 2，以显示与所连接的设备关联的信息的位掩码。

   ```dbgcmd 
   0: kd> !drvobj \Driver\sysvad_tabletaudiosample 2
   Driver object (ffffe0008834f670) is for:
   \Driver\sysvad_tabletaudiosample
   DriverEntry:   fffff80114b45310  tabletaudiosample!FxDriverEntry
   DriverStartIo: 00000000 
   DriverUnload:  fffff80114b5fea0                tabletaudiosample!DriverUnload
   AddDevice:     fffff80114b5f000  tabletaudiosample!AddDevice

   Dispatch routines:
   [00] IRP_MJ_CREATE                      fffff80117b49a20             portcls!DispatchCreate
   [01] IRP_MJ_CREATE_NAMED_PIPE           fffff8015a949a00          nt!IopInvalidDeviceRequest
   [02] IRP_MJ_CLOSE                       fffff80115e26f90                ks!DispatchCleanup
   [03] IRP_MJ_READ                        fffff80115e32710                ks!DispatchRead
   [04] IRP_MJ_WRITE                       fffff80115e327e0              ks!DispatchWrite
   [05] IRP_MJ_QUERY_INFORMATION           fffff8015a949a00         nt!IopInvalidDeviceRequest
   [06] IRP_MJ_SET_INFORMATION             fffff8015a949a00              nt!IopInvalidDeviceRequest
   [07] IRP_MJ_QUERY_EA                    fffff8015a949a00         nt!IopInvalidDeviceRequest
   [08] IRP_MJ_SET_EA                      fffff8015a949a00              nt!IopInvalidDeviceRequest
   [09] IRP_MJ_FLUSH_BUFFERS               fffff80115e32640  ks!DispatchFlush
   [0a] IRP_MJ_QUERY_VOLUME_INFORMATION    fffff8015a949a00           nt!IopInvalidDeviceRequest
   [0b] IRP_MJ_SET_VOLUME_INFORMATION      fffff8015a949a00               nt!IopInvalidDeviceRequest
   [0c] IRP_MJ_DIRECTORY_CONTROL           fffff8015a949a00           nt!IopInvalidDeviceRequest
   [0d] IRP_MJ_FILE_SYSTEM_CONTROL         fffff8015a949a00         nt!IopInvalidDeviceRequest
   [0e] IRP_MJ_DEVICE_CONTROL              fffff80115e27480               ks!DispatchDeviceIoControl
   [0f] IRP_MJ_INTERNAL_DEVICE_CONTROL     fffff8015a949a00   nt!IopInvalidDeviceRequest
   [10] IRP_MJ_SHUTDOWN                    fffff8015a949a00      nt!IopInvalidDeviceRequest
   [11] IRP_MJ_LOCK_CONTROL                fffff8015a949a00  nt!IopInvalidDeviceRequest
   [12] IRP_MJ_CLEANUP                     fffff8015a949a00           nt!IopInvalidDeviceRequest
   [13] IRP_MJ_CREATE_MAILSLOT             fffff8015a949a00               nt!IopInvalidDeviceRequest
   [14] IRP_MJ_QUERY_SECURITY              fffff80115e326a0 ks!DispatchQuerySecurity
   [15] IRP_MJ_SET_SECURITY                fffff80115e32770      ks!DispatchSetSecurity
   [16] IRP_MJ_POWER                       fffff80117b3dce0            portcls!DispatchPower
   [17] IRP_MJ_SYSTEM_CONTROL              fffff80117b13d30              portcls!PcWmiSystemControl
   [18] IRP_MJ_DEVICE_CHANGE               fffff8015a949a00 nt!IopInvalidDeviceRequest
   [19] IRP_MJ_QUERY_QUOTA                 fffff8015a949a00  nt!IopInvalidDeviceRequest
   [1a] IRP_MJ_SET_QUOTA                   fffff8015a949a00       nt!IopInvalidDeviceRequest
   [1b] IRP_MJ_PNP                         fffff80114b5f7d0 tabletaudiosample!PnpHandler
   ```

6. 输入 **！ devstack**<em>&lt;PDO 地址&gt;</em>命令以显示与设备驱动程序相关联的插信息。 中显示的输出 **！ devnode 0 1**命令包含与正在运行的驱动程序实例关联的 PDO 地址。 在此示例很*0xffffe00089c575a0*。 使用 PDO 解决 **！ devnode**显示在您 PC 上，不是如下所示。

   ```dbgcmd
   0: kd> !devstack 0xffffe00089c575a0
     !DevObj           !DrvObj            !DevExt           ObjectName
     ffffe00088d212e0  \Driver\ksthunk    ffffe00088d21430  0000007b
     ffffe00088386a50  \Driver\sysvad_tabletaudiosampleffffe00088386ba0  0000007a
   > ffffe00089c575a0  \Driver\PnpManager 00000000  0000004e
   !DevNode ffffe00086e68190 :
     DeviceInst is "ROOT\sysvad_TabletAudioSample\0000"
     ServiceName is "sysvad_tabletaudiosample"
   ```

输出显示有 farily 简单的设备驱动程序堆栈。 Sysvad\_TabletAudioSample 驱动程序是 PnPManager 节点的子节点。 PnPManager 是根节点。

下图显示了更复杂的设备节点树。

![设备有大约具有 20 个节点的节点树](images/debuglab-image-device-node-tree.png)

**请注意**  有关更复杂的驱动程序堆栈的详细信息，请参阅[驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/hh439632)并[设备节点和设备堆栈](https://msdn.microsoft.com/library/windows/hardware/ff554721)。

 

## <a name="span-idworkingwithbreakpointsspansection-7-working-with-breakpoints"></a><span id="workingwithbreakpoints"></span>第 7 部分：使用断点


*第 7 节中将使用断点来中断代码执行的特定点上。*

**使用命令设置断点**

使用断点来中断代码执行一个特定的代码行。 你可以然后单步前进在代码中从该点，若要调试该特定代码部分。

若要设置使用调试命令断点，请使用以下值之一**b**命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>bp</p></td>
<td align="left"><p>设置断点将处于活动状态，直到卸载的模块。</p></td>
</tr>
<tr class="even">
<td align="left"><p>bu</p></td>
<td align="left"><p>设置断点时该模块卸载并重新启用时重新加载该模块未经解析。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bm</p></td>
<td align="left"><p>设置符号的断点。 此命令将适当地使用 bu 或最佳实践，并允许通配符 * 以用于在每个符号相匹配 （如在类中的所有方法） 上设置断点。</p></td>
</tr>
</tbody>
</table>

 

1.  使用 WinDbg UI 以确认**调试** &gt; **源模式**当前 WinDbg 会话中启用。

2.  通过键入以下命令将你的本地代码位置添加到源路径。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

3.  通过键入以下命令将你的本地符号位置添加到符号路径。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

4.  **设置调试掩码**

    你正在使用的驱动程序，它可能会比较方便查看所有可能显示的消息。 以下内容，以更改默认调试位掩码，以便所有调试从目标系统的消息将显示在调试器中的类型。

    ```dbgcmd
    0: kd> ed nt!Kd_DEFAULT_MASK 0xFFFFFFFF
    ```

5.  设置的断点**bm**命令中使用的驱动程序后, 跟函数名称 (AddDevice) 想要设置断点，名称由一个感叹号分隔。

    ```dbgcmd
    0: kd> bm tabletaudiosample!AddDevice
    breakpoint 1 redefined
      1: fffff801`14b5f000 @!"tabletaudiosample!AddDevice"
    ```

    可以使用不同的语法与设置变量，如结合&lt;模块&gt;！&lt;符号&gt;，&lt;类&gt;::&lt;方法&gt;，&lt;file.cpp&gt;:&lt;行号&gt;，或跳过数乘以&lt;条件&gt; &lt; \# &gt;。 有关详细信息，请参阅[使用断点](using-breakpoints.md)。

6.  列出要确认通过键入来设置了断点的当前断点**bl**命令。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`14b5f000     0001 (0001) tabletaudiosample!AddDevice
    ```

7.  通过键入 go 命令重新启动目标系统上的执行代码**g**。

8.  **-&gt;在目标系统上**

    在 Windows 中，打开设备管理器使用的图标，或输入**mmc devmgmt.msc**。 在中**设备管理器**展开**声音、 视频和游戏控制器**节点。 右键单击虚拟音频驱动程序条目，然后选择**禁用**菜单中。

9.  右键单击虚拟音频驱动程序条目，然后选择**启用**菜单中。
10. **&lt;在主机系统**

    这应该会导致重新加载驱动程序，可以调用 AddDevice 的 Windows。 这将导致 AddDevice 调试断点，以触发，并且在目标系统上的驱动程序代码的执行应暂停。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!AddDevice:
    fffff801`14baf000 4889542410      mov     qword ptr [rsp+10h],rdx
    ```

    如果您的源路径设置正确，应在 adapter.cpp AddDevice 例程处停止

    ```dbgcmd
    {
        PAGED_CODE();

        NTSTATUS        ntStatus;
        ULONG           maxObjects;

        DPF(D_TERSE, ("[AddDevice]"));

        maxObjects = g_MaxMiniports;
        
        #ifdef SYSVAD_BTH_BYPASS
        // 
        // Allow three (3) Bluetooth hands-free profile devices.
        //
        maxObjects += g_MaxBthHfpMiniports * 3; 
        #endif // SYSVAD_BTH_BYPASS

        // Tell the class driver to add the device.
        //
        ntStatus = 
            PcAddAdapterDevice
            ( 
                DriverObject,
                PhysicalDeviceObject,
                PCPFNSTARTDEVICE(StartDevice),
                maxObjects,
                0
            );
        return ntStatus;
    } // AddDevice
    ```

11. 单步通过逐行执行代码通过键入**p**命令或按 F10。 您可以跳出向前 sysvad AddDevice 代码到 PpvUtilCall，PnpCallAddDevice，再到 PipCallDriverAddDevice Windows 代码。 你可以提供到的数字**p**命令来单步前进多行，例如*p 5*。

12. 完成后单步执行代码，使用 go 命令**g**重启目标系统上的执行。

**设置访问断点的内存**

此外可以设置触发访问的内存位置时的断点。 使用**ba** （换行的访问权限） 命令，使用以下语法。

```dbgcmd
ba <access> <size> <address> {options}
```

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">选项</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>E</p></td>
<td align="left"><p>执行 （时 CPU 会从地址中提取一条指令）</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>读/写 （时 CPU 读取或写入到的地址）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>W</p></td>
<td align="left"><p>写入 （当 CPU 将写入地址）</p></td>
</tr>
</tbody>
</table>

 

请注意，在任何给定时间只能设置四个数据断点，它将由您来确保将正确对齐数据或将不会触发该断点 （字必须以整除的地址结尾的一半，dword 值必须是整除 4和四字的 0 或 8)

例如，若要设置特定的内存地址的读/写断点，请使用如下命令。

```dbgcmd
ba r 4 fffff800`7bc9eff0
```

**修改断点的状态**

可以使用以下命令来修改现有断点。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>bl</p></td>
<td align="left"><p>列出断点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>bc</p></td>
<td align="left"><p>清除列表中的断点。 使用 bc * 若要清除所有断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bd</p></td>
<td align="left"><p>禁用断点。 使用 bd * 若要禁用所有断点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>将</p></td>
<td align="left"><p>启用断点。 使用 * 若要启用所有断点。</p></td>
</tr>
</tbody>
</table>

 

或者，您还可以通过单击修改断点**编辑** &gt; **断点**。 请注意，断点对话框仅适用于现有断点。 必须从命令行设置新断点。

**MixerVolume 上设置断点**

音频驱动程序代码的不同部分调用以响应各种事件，设备驱动程序加载之后。 在下一步部分中，我们设置当用户调整虚拟的音频驱动程序的音量控制时将触发一个断点。

若要在 MixerVolume 上设置断点，请执行以下步骤。

1.  **&lt;在主机系统**

    若要查找更改卷的方法，使用 x 命令列出 CAdapterCommon，包含字符串卷的符号。

    ```dbgcmd
    kd> x tabletaudiosample!CAdapterCommon::*
    ...
    fffff800`7bce26a0 tabletaudiosample!CAdapterCommon::MixerVolumeWrite (unsigned long, unsigned long, long)
    …
    ```

    使用 CTRL + F 在卷的输出中向上搜索并找到 MixerVolumeWrite 方法。

2.  清除上一个断点使用 bc \*。
3.  使用以下命令的 CAdapterCommon::MixerVolumeWrite 例程上设置符号断点。

    ```dbgcmd
    kd> bm tabletaudiosample!CAdapterCommon::MixerVolumeWrite
      1: fffff801`177b26a0 @!"tabletaudiosample!CAdapterCommon::MixerVolumeWrite"
    ```

4.  列出要确认正确设置了断点的断点。

    ```dbgcmd
    kd> bl
    1 e fffff801`177b26a0 [c:\WDK_Samples\audio\sysvad\common.cpp @ 1668]    0001 (0001) tabletaudiosample!CAdapterCommon::MixerVolumeWrite
    ```

5.  通过键入 go 命令重新启动目标系统上的执行代码**g**。

6.  在控制面板中，选择**硬件和声音** &gt;**声音**。 右键单击**接收器说明示例**，然后选择**属性**。 选择**级别**选项卡。调整滑块卷。

7.  这应该会导致 SetMixerVolume 调试断点，以触发，并且在目标系统上的驱动程序代码的执行应暂停。

    ```dbgcmd
    kd> g
    Breakpoint 1 hit
    tabletaudiosample!CAdapterCommon::MixerVolumeWrite:
    fffff801`177b26a0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    应在此行中 common.cpp 处停止

    ```dbgcmd
    {
        if (m_pHW)
        {
            m_pHW->SetMixerVolume(Index, Channel, Value);
        }
    } // MixerVolumeWrite
    ```

8.  使用 dv 命令显示当前变量和值。 在本实验的下一节中提供对变量的详细信息。

    ```dbgcmd
    2: kd> dv
               this = 0x00000000`00000010
             ulNode = 0x344
          ulChannel = 0x210a45f8
            lVolume = 0n24
    ```

9.  按**F10**单步执行代码。

10. 按**F5**完成 MixerVolumeWrite 代码的执行。

**摘要-在调试器命令窗口中逐句通过代码**

以下是可以使用的命令来逐句通过代码 （具有关联的键盘快捷方式显示在括号中）。

-   中断 (Ctrl + Break)-此命令将中断一个系统，只要系统正在运行，并且是与 WinDbg （内核调试程序中的序列是 Ctrl + C） 的通信中。

-   步跃 (f10) – 此命令将导致代码执行来继续执行一个语句或一次一条指令。 如果遇到调用，代码执行将通过调用而无需输入调用的例程。 (如果编程语言为 C 或 c + +，WinDbg 为源模式中，源模式可以打开或关闭使用**调试**&gt;**源模式**)。

-   步骤中 (F11)-此命令是逐过程类似，只不过调用的执行将进入被调用例程。

-   跳出 (Shift + F11) – 此命令将导致执行运行并从当前退出例程 （调用堆栈中的当前位置）。 这是很有用，如果您已了解足够多的例程。

-   运行到光标处 （F7 或 Ctrl + F10） – 将光标放在源代码或反汇编窗口中要执行中断操作，然后按 F7;执行代码将运行到该点。 请注意，如果代码执行流不会达到由光标指示的点 （例如，IF 语句不执行了），WinDbg 将不会中断，因为代码执行未到达指定的点。

-   运行 (F5) – 运行直到遇到断点时或发生的 bug 检查之类的事件发生。

**高级选项**

-   设置指令到当前行 （Ctrl + Shift + I）-在源窗口中，你可以将光标放在行上，输入此键盘快捷方式，并执行代码将从该点开始，就立即让它继续操作 （例如，使用 F5 或 F10）。 如果你想要重试一个序列，但它需要非常谨慎，这非常方便。 例如，寄存器和变量未设置为应执行代码是否有自然地达到该行。

-   直接设置的 eip 寄存器-你可以将值放到 eip 寄存器，并立即按 F5 (或 F10、 F11，等等)，从该地址开始执行。 只是指定的程序集指令的地址，这是类似于将指令设置为游标指定当前行。

它可能更容易到步骤通过用户界面而不是从命令行因此建议使用此方法。 如果有必要，请使用以下命令可以通过在命令行的源代码文件的步骤：

-   .lines-启用源代码行信息。

-   最佳实践主要的模块的开始处设置初始断点。

-   l + t-则将由源行完成单步执行。

-   选择**调试**&gt;**源模式**输入源模式;`L+t`命令是不够的。

-   l + s 的源行将显示在提示符处。

-   g-运行程序直到输入"main"。

-   p-执行一个源行。

有关详细信息，请参阅[源代码调试在 WinDbg 中](source-window.md)调试的参考文档中。

**代码中设置断点**

可以在代码中设置断点，通过添加`DebugBreak()`语句并重新生成项目并重新安装该驱动程序。 此断点将激发每次启用驱动程序，以便您可以在早期开发阶段，不是在生产代码中使用的技术。 此方法不是灵活性不如动态设置使用断点命令断点。

提示：您可能想要保留一份 Sysvad 驱动程序和扩展进行进一步的实验室工作添加断点。

1.  设置要发生 AddDevice 方法运行通过添加每次中断`DebugBreak()`语句的示例代码。

    ```dbgcmd
    ...
        // Insert the DebugBreak() statment before the  PcAddAdapterDevice is called.
        //

        DebugBreak()
        
        // Tell the class driver to add the device.
        //
        ntStatus = 
            PcAddAdapterDevice
            ( 
                DriverObject,
                PhysicalDeviceObject,
                PCPFNSTARTDEVICE(StartDevice),
                maxObjects,
                0
            );

        return ntStatus;
    } // AddDevice
    ```

2.  遵循所有前面所述重新生成 Microsoft Visual Studio 中的驱动程序并重新将其安装到目标计算机的步骤。 请务必在安装更新的驱动程序之前卸载现有的驱动程序。
3.  清除任何以前的断点，并确保将调试器附加到目标 PC。

4.  当代码在运行，并且达到`DebugBreak`语句中，将停止执行，将显示一条消息。

    ```dbgcmd
    KERNELBASE!DebugBreak:
    77b3b770 defe     __debugbreak
    ```

## <a name="span-idlookingatvariablesspanspan-idlookingatvariablesspanspan-idlookingatvariablesspansection-8-display-variables"></a><span id="LookingAtVariables"></span><span id="lookingatvariables"></span><span id="LOOKINGATVARIABLES"></span>第 8 部分：显示变量


*在第 8 节，你将使用调试器命令来显示变量。*

它可用于检查变量，代码执行来确认代码按预期方式工作。 此实验室从而检查变量，如音频驱动程序发出声音。

1.  使用**dv**命令，检查与 tabletaudiosample 关联的区域设置变量 ！CMiniportWaveRT::New\*。

    ```dbgcmd
    kd> dv tabletaudiosample!CMiniportWaveRT::New*
    ```

2.  清除上一个断点

    ```dbgcmd
    bc *
    ```

3.  使用以下命令的 CMiniportWaveCyclicStreamMSVAD 例程上设置符号断点。

    ```dbgcmd
    0: kd> bm tabletaudiosample!CMiniportWaveRT::NewStream
      1: fffff801`177dffc0 @!"tabletaudiosample!CMiniportWaveRT::NewStream"
    ```

4.  通过键入 go 命令重新启动目标系统上的执行代码**g**。

5.  **-&gt; 在目标系统上**

    找到小型媒体文件 （如 Windows 会通知声音文件扩展名为.wav 的文件） 并单击要播放的文件。 例如，你可以使用 Ring05.wav 位于 Windows\\媒体目录。

6.  **&lt;在主机系统**

    时，将会播放媒体文件，应触发断点，并在目标系统上的驱动程序代码的执行应暂停。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::NewStream:
    fffff801`177dffc0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    源代码窗口应该会突出显示上进行 NewStream 函数入口的大括号。

    ```dbgcmd
    /*++

    Routine Description:

      The NewStream function creates a new instance of a logical stream 
      associated with a specified physical channel. Callers of NewStream should 
      run at IRQL PASSIVE_LEVEL.

    Arguments:

      OutStream -

      OuterUnknown -

      Pin - 

      Capture - 

      DataFormat -

    Return Value:

      NT status code.

    --*/
    {

    ...
    ```

7.  **本地变量**

    可以通过键入显示的名称和值的给定的框架的所有局部变量**dv**命令。

    ```dbgcmd
    0: kd> dv
                    this = 0xffffe000`4436f8e0
               OutStream = 0xffffe000`49d2f130
            OuterUnknown = 0xffffe000`4436fa30
                     Pin = 0
                 Capture = 0x01 '
              DataFormat = 0xffffe000`44227790
    signalProcessingMode = {487E9220-E000-FFFF-30F1-D24900E0FFFF}
                ntStatus = 0n1055
                  stream = 0x00000000`00000200
    ```

8.  **使用 DML 来显示变量**

    若要使用 DML 浏览变量，请单击带下划线的元素。 单击操作生成[ **dx （显示 NatVis 表达式）** ](dx--display-visualizer-variables-.md)命令，您可以向下钻取嵌套数据结构。

    ```dbgcmd
    0: kd> dx -r1 (*((tabletaudiosample!CMiniportWaveRT *)0xffffe001d10b8380))
    (*((tabletaudiosample!CMiniportWaveRT *)0xffffe001d10b8380)) :  [Type: CMiniportWaveRT]
        [+0x020] m_lRefCount      : 0
        [+0x028] m_pUnknownOuter  : 0xffffe001d1477e50 : [Type: IUnknown *]
        [+0x030] m_ulLoopbackAllocated : 0x2050
        [+0x034] m_ulSystemAllocated : 0x180
        [+0x038] m_ulOffloadAllocated : 0x0
        [+0x03c] m_dwCaptureAllocatedModes : 0x0

    0: kd> dx -r1 (*((tabletaudiosample!_GUID *)0xffffd001c8acd348))
    (*((tabletaudiosample!_GUID *)0xffffd001c8acd348)) : {487E9220-E000-FFFF-30F1-D24900E0FFFF} [Type: _GUID]
        [<Raw View>]    

    0: kd> dx -r1 -n (*((tabletaudiosample!_GUID *)0xffffd001c8acd348))
    (*((tabletaudiosample!_GUID *)0xffffd001c8acd348)) :  [Type: _GUID]
        [+0x000] Data1            : 0x487e9220
        [+0x004] Data2            : 0xe000
        [+0x006] Data3            : 0xffff
        [+0x008] Data4            :  [Type: unsigned char [8]]

    0: kd> dx -r1 -n (*((tabletaudiosample!unsigned char (*)[8])0xffffd001c8acd350))
    (*((tabletaudiosample!unsigned char (*)[8])0xffffd001c8acd350)) :  [Type: unsigned char [8]]
        [0]              : 0x30
        [1]              : 0xf1
        [2]              : 0xd2
        [3]              : 0x49
        [4]              : 0x0
        [5]              : 0xe0
        [6]              : 0xff
        [7]              : 0xff
    ```

9.  **全局变量**

    也可以键入找到的全局变量的内存位置 **？&lt;变量名&gt;**。

    ```dbgcmd
    0: kd> ? signalProcessingMode
    Evaluate expression: -52768896396472 = ffffd001`c8acd348
    ```

10. 这将返回的内存位置的变量，在这种情况下*ffffd001\`c8acd348*。 可以通过转储的该位置键入值查看内存位置的内容**dd**命令使用前一命令返回的内存位置。

    ```dbgcmd
    0: kd> dd ffffd001`c8acd348
    ffffd001`c8acd348  487e9220 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd358  4837c468 ffffe000 18221570 ffffc000
    ffffd001`c8acd368  4436f8e0 ffffe000 487e9220 ffffe000
    ffffd001`c8acd378  18ab145b fffff801 4837c420 ffffe000
    ffffd001`c8acd388  4436f8e0 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd398  4436fa30 ffffe000 00000000 00000000
    ffffd001`c8acd3a8  00000001 00000000 44227790 ffffe000
    ffffd001`c8acd3b8  18adc7f9 fffff801 495972a0 ffffe000
    ```

11. 此外可以使用变量名称与**dd**命令。

    ```dbgcmd
    0: kd> dd signalProcessingMode
    ffffd001`c8acd348  487e9220 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd358  4837c468 ffffe000 18221570 ffffc000
    ffffd001`c8acd368  4436f8e0 ffffe000 487e9220 ffffe000
    ffffd001`c8acd378  18ab145b fffff801 4837c420 ffffe000
    ffffd001`c8acd388  4436f8e0 ffffe000 49d2f130 ffffe000
    ffffd001`c8acd398  4436fa30 ffffe000 00000000 00000000
    ffffd001`c8acd3a8  00000001 00000000 44227790 ffffe000
    ffffd001`c8acd3b8  18adc7f9 fffff801 495972a0 ffffe000
    ```

12. **显示变量**

    使用**视图**&gt; **局部变量**菜单项以显示本地变量。 此接口还提供了此向下钻取更复杂的数据结构的能力。

    ![windbg 显示示例代码局部变量和命令窗口](images/sysvad-lab-display-variables.png)

13. 使用 p 或 f10 单步执行代码中的正向大约有 10 个行，直到突出显示 ntStatus = IsFormatSupported (Pin、 捕获，DataFormat);代码行。

    ```cpp
        PAGED_CODE();

        ASSERT(OutStream);
        ASSERT(DataFormat);

        DPF_ENTER(("[CMiniportWaveRT::NewStream]"));

        NTSTATUS                    ntStatus = STATUS_SUCCESS;
        PCMiniportWaveRTStream      stream = NULL;
        GUID                        signalProcessingMode = AUDIO_SIGNALPROCESSINGMODE_DEFAULT;
        
        *OutStream = NULL;

         //
        // If the data format attributes were specified, extract them.
        //
        if ( DataFormat->Flags & KSDATAFORMAT_ATTRIBUTES )
        {
            // The attributes are aligned (QWORD alignment) after the data format
            PKSMULTIPLE_ITEM attributes = (PKSMULTIPLE_ITEM) (((PBYTE)DataFormat) + ((DataFormat->FormatSize + FILE_QUAD_ALIGNMENT) & ~FILE_QUAD_ALIGNMENT));
            ntStatus = GetAttributesFromAttributeList(attributes, attributes->Size, &signalProcessingMode);
        }

        // Check if we have enough streams.
        //
        if (NT_SUCCESS(ntStatus))
        {
            ntStatus = ValidateStreamCreate(Pin, Capture, signalProcessingMode);
        }

        // Determine if the format is valid.
        //
        if (NT_SUCCESS(ntStatus))
        {
            ntStatus = IsFormatSupported(Pin, Capture, DataFormat);
        }

    ...
    ```

14. 使用**dv**命令以显示的名称和值的给定的框架的所有本地变量。 请注意，按预期方式的值不同于上次我们运行此命令中，其他代码均已运行，本地变量和某些变量的更改现在不在当前帧或其值已更改。

    ```dbgcmd
    2: kd> dv
                    this = 0xffffe001`d1182000
               OutStream = 0xffffe001`d4776d20
            OuterUnknown = 0xffffe001`d4776bc8
                     Pin = 0
                 Capture = 0x00 '
              DataFormat = 0xffffe001`cd7609b0
    signalProcessingMode = {4780004E-7133-41D8-8C74-660DADD2C0EE}
                ntStatus = 0n0
                  stream = 0x00000000`00000000
    ```

## <a name="span-idviewingcallstacksspansection-9-view-call-stacks"></a><span id="viewingcallstacks"></span>第 9 部分：查看调用堆栈


*在第 9 节，可查看调用堆栈，以检查调用方/杨柳代码。*

调用堆栈是导致程序计数器当前位置的函数调用链。 在调用堆栈顶部的函数是当前函数，而下一步函数调用当前函数的函数，等等。

若要显示调用堆栈，请使用 k\*命令：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>kb</p></td>
<td align="left"><p>显示堆栈和前三个参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>kp</p></td>
<td align="left"><p>显示堆栈和参数的完整列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>kn</p></td>
<td align="left"><p>可以看到它旁边的帧信息堆栈。</p></td>
</tr>
</tbody>
</table>

 

如果你想要保留可用的调用堆栈，则可以单击**视图**&gt; **调用堆栈**查看它。 单击可切换的附加信息显示在窗口顶部的列。

![windbg 在调用堆栈窗口](images/sysvad-lab-call-stack.png)

调试示例适配器代码中中断状态时，此输出显示调用堆栈。

```dbgcmd
0: kd> kb
# RetAddr           : Args to Child                                                           : Call Site
00 fffff800`7a0fa607 : ffffe001`d1182000 ffffe001`d4776d20 ffffe001`d4776bc8 ffffe001`00000000 : tabletaudiosample!CMiniportWaveRT::NewStream+0x1dc [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 597]
01 fffff800`7a0fb2c3 : 00000000`00000000 ffffe001`d122bb10 ffffe001`ceb81750 ffffe001`d173f058 : portcls!CPortPinWaveRT::Init+0x2e7
02 fffff800`7a0fc7f9 : ffffe001`d4776bc0 00000000`00000000 ffffe001`d10b8380 ffffe001`d122bb10 : portcls!CPortFilterWaveRT::NewIrpTarget+0x193
03 fffff800`7a180552 : 00000000`00000000 ffffe001`d10b8380 ffffe001`d122bb10 ffffe001`d4565600 : portcls!xDispatchCreate+0xd9
04 fffff800`7a109a9a : ffffe001`d10b84d0 ffffe001`d10b8380 00000000`00000000 ffffe001`00000000 : ks!KsDispatchIrp+0x272
05 fffff800`7bd314b1 : ffffe001`d122bb10 ffffd001`c3098590 ffffe001`d122bd90 ffffe001`ce80da70 : portcls!DispatchCreate+0x7a
06 fffff803`cda1bfa8 : 00000000`00000024 00000000`00000000 00000000`00000000 ffffe001`d122bb10 : ksthunk!CKernelFilterDevice::DispatchIrp+0xf9
07 fffff803`cda7b306 : 00000000`000001f0 ffffe001`d48ce690 ffffe001`d13d6400 ffffe001`d13d64c0 : nt!IopParseDevice+0x7c8
08 fffff803`cda12916 : 00000000`000001f0 ffffd001`c30988d0 ffffe001`d13d6490 fffff803`cda7b250 : nt!IopParseFile+0xb6
09 fffff803`cda1131c : ffffe001`d2ccb001 ffffd001`c30989e0 00ffffe0`00000040 ffffe001`cd127dc0 : nt!ObpLookupObjectName+0x776
0a fffff803`cd9fedb8 : ffffe001`00000001 ffffe001`d48ce690 00000000`00000000 00000000`00000000 : nt!ObOpenObjectByNameEx+0x1ec
0b fffff803`cd9fe919 : 000000ee`6d1fc8d8 000000ee`6d1fc788 000000ee`6d1fc7e0 000000ee`6d1fc7d0 : nt!IopCreateFile+0x3d8
0c fffff803`cd752fa3 : ffffc000`1f296870 fffff803`cd9d9fbd ffffd001`c3098be8 00000000`00000000 : nt!NtCreateFile+0x79
0d 00007fff`69805b74 : 00007fff`487484e6 0000029b`00000003 00000000`0000012e 00000000`00000000 : nt!KiSystemServiceCopyEnd+0x13
0e 00007fff`487484e6 : 0000029b`00000003 00000000`0000012e 00000000`00000000 00000000`00000000 : 0x00007fff`69805b74
0f 0000029b`00000003 : 00000000`0000012e 00000000`00000000 00000000`00000000 00000000`00000000 : 0x00007fff`487484e6
10 00000000`0000012e : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000080 : 0x0000029b`00000003
11 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000080 00000000`00000000 : 0x12e
```

可以使用 DML 若要进一步探索代码。 当您单击的第一次 00 条目时[ **.frame （设置本地上下文）** ](-frame--set-local-context-.md)命令用于设置上下文，然后[ **dv （显示本地变量）**](dv--display-local-variables-.md)命令显示本地变量。

```dbgcmd
0: kd> .frame 0n0;dv /t /v
00 ffffd001`c30981d0 fffff800`7a0fa607 tabletaudiosample!CMiniportWaveRT::NewStream+0x1dc [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 597]
ffffd001`c30982b0 class CMiniportWaveRT * this = 0xffffe001`d1182000
ffffd001`c30982b8 struct IMiniportWaveRTStream ** OutStream = 0xffffe001`d4776d20
ffffd001`c30982c0 struct IPortWaveRTStream * OuterUnknown = 0xffffe001`d4776bc8
ffffd001`c30982c8 unsigned long Pin = 0
ffffd001`c30982d0 unsigned char Capture = 0x00 '
ffffd001`c30982d8 union KSDATAFORMAT * DataFormat = 0xffffe001`cd7609b0
ffffd001`c3098270 struct _GUID signalProcessingMode = {4780004E-7133-41D8-8C74-660DADD2C0EE}
ffffd001`c3098210 long ntStatus = 0n0
ffffd001`c3098218 class CMiniportWaveRTStream * stream = 0x00000000`00000000
```

## <a name="span-iddisplayingprocessesandthreadsspansection-10-display-processes-and-threads"></a><span id="displayingprocessesandthreads"></span>第 10 部分：显示进程和线程


*在部分 10 中，将使用调试器命令以显示进程和线程。*

**进程**

若要更改当前进程上下文，请使用.process&lt;进程&gt;命令。 下面的示例演示如何标识的进程和上下文切换到它。

-   使用`!process`命令以显示当前所涉及的进程中播放声音。

    有关详细信息请参阅[ **！ 过程**](-process.md)

该输出显示过程都与 audiodg.exe 关联。 如果您仍在本主题前面部分所述的断点处，当前进程应使用 audiodg.exe 映像相关联。

**&lt;在主机系统**

```dbgcmd
0: kd> !process
PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
    VadRoot ffffe001d4222f70 Vads 70 Clone 0 Private 504. Modified 16. Locked 0.
    DeviceMap ffffc00019113080
    Token                             ffffc0001f1d4060
    ElapsedTime                       <Invalid>
    UserTime                          00:00:00.000
    KernelTime                        00:00:00.000
    QuotaPoolUsage[PagedPool]         81632
    QuotaPoolUsage[NonPagedPool]      9704
    Working Set Sizes (now,min,max)  (2154, 1814, 2109) (8616KB, 7256KB, 8436KB)
    PeakWorkingSetSize                2101
    VirtualSize                       2097192 Mb
    PeakVirtualSize                   2097192 Mb
    PageFaultCount                    2336
    MemoryPriority                    BACKGROUND
    BasePriority                      8
    CommitCharge                      1573

        THREAD ffffe001d173e840  Cid 10f0.1dac  Teb: 000000ee6cf8b000 Win32Thread: ffffe001d1118cf0 WAIT: (UserRequest) UserMode Non-Alertable
            ffffe001d16c4dd0  NotificationEvent
            ffffe001d08b0840  ProcessObject

        THREAD ffffe001ceb77080  Cid 10f0.16dc  Teb: 000000ee6cf8d000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001cf2d1840  QueueObject

        THREAD ffffe001d112c840  Cid 10f0.0a4c  Teb: 000000ee6cf8f000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001cf2d1840  QueueObject

        THREAD ffffe001d16c7840  Cid 10f0.13c4  Teb: 000000ee6cf91000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001cf2d1840  QueueObject

        THREAD ffffe001cec67840  Cid 10f0.0dbc  Teb: 000000ee6cf93000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d173e5c0  QueueObject

        THREAD ffffe001d1117840  Cid 10f0.1d6c  Teb: 000000ee6cf95000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d173e5c0  QueueObject

        THREAD ffffe001cdeae840  Cid 10f0.0298  Teb: 000000ee6cf97000 Win32Thread: 0000000000000000 RUNNING on processor 2
```

请注意，一个与此进程关联的线程都处于运行状态。 此线程已支持播放媒体剪辑时命中了断点。

使用 **！ process 0 0**命令以显示所有进程的摘要信息。 在命令输出使用 CTRL + F 来查找与 audiodg.exe 映像关联的进程的进程 ID。 在如下所示示例中，进程 ID 是*ffffe001d147c840*。

在您的 PC 以更高版本在此实验室中使用 audiodg.exe 与关联的记录进程 ID。 \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

```dbgcmd
...

PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
...
```

输入 g 到调试器中运行代码前滚直到完成媒体剪辑播放。 然后到调试器中断通过按 Ctrl + ScrLk (Ctrl + Break) 使用 ！ 处理命令，确认您当前正在运行不同的进程。

```dbgcmd
!process
PROCESS ffffe001cd0ad040
    SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
    DirBase: 001aa000  ObjectTable: ffffc00017214000  HandleCount: <Data Not Accessible>
    Image: System
    VadRoot ffffe001d402b820 Vads 438 Clone 0 Private 13417. Modified 87866. Locked 64.
    DeviceMap ffffc0001721a070
    Token                             ffffc00017216a60
    ElapsedTime                       05:04:54.716
    UserTime                          00:00:00.000
    KernelTime                        00:00:20.531
    QuotaPoolUsage[PagedPool]         0
    QuotaPoolUsage[NonPagedPool]      0
    Working Set Sizes (now,min,max)  (1720, 50, 450) (6880KB, 200KB, 1800KB)
    PeakWorkingSetSize                15853
    VirtualSize                       58 Mb
    PeakVirtualSize                   74 Mb
    PageFaultCount                    46128
   MemoryPriority                    BACKGROUND
    BasePriority                      8
    CommitCharge                      66

        THREAD ffffe001cd0295c0  Cid 0004.000c  Teb: 0000000000000000 Win32Thread: 0000000000000000 WAIT: (Executive) KernelMode Non-Alertable
            fffff803cd8e0120  SynchronizationEvent

        THREAD ffffe001cd02a6c0  Cid 0004.0010  Teb: 0000000000000000 Win32Thread: 0000000000000000 WAIT: (Executive) KernelMode Non-Alertable
            fffff803cd8e0ba0  Semaphore Limit 0x7fffffff
...
```

上面的输出中显示的不同系统进程*ffffe001cd0ad040*正在运行。 映像名称将显示系统中，不 audiodg.exe。

现在，使用 ！ 处理命令以切换到与 audiodg.exe 相关联的进程。 在示例中，进程 ID 是*ffffe001d147c840*。 替换为您的进程 id，之前记录在示例中的进程 ID。

```dbgcmd
0: kd> !process  ffffe001d147c840
PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
    VadRoot ffffe001d4222f70 Vads 60 Clone 0 Private 299. Modified 152. Locked 0.
    DeviceMap ffffc00019113080
    Token                             ffffc0001f1d4060
    ElapsedTime                       1 Day 01:53:14.490
    UserTime                          00:00:00.031
    KernelTime                        00:00:00.031
    QuotaPoolUsage[PagedPool]         81552
    QuotaPoolUsage[NonPagedPool]      8344
    Working Set Sizes (now,min,max)  (1915, 1814, 2109) (7660KB, 7256KB, 8436KB)
    PeakWorkingSetSize                2116
    VirtualSize                       2097189 Mb
    PeakVirtualSize                   2097192 Mb
    PageFaultCount                    2464
    MemoryPriority                    BACKGROUND
    BasePriority                      8
    CommitCharge                      1418

        THREAD ffffe001d173e840  Cid 10f0.1dac  Teb: 000000ee6cf8b000 Win32Thread: ffffe001d1118cf0 WAIT: (UserRequest) UserMode Non-Alertable
            ffffe001d16c4dd0  NotificationEvent
            ffffe001d08b0840  ProcessObject
        Not impersonating
        DeviceMap                 ffffc00019113080
        Owning Process            ffffe001d147c840       Image:         audiodg.exe
        Attached Process          N/A            Image:         N/A
        Wait Start TickCount      338852         Ticks: 197682 (0:00:51:28.781)
        Context Switch Count      36             IdealProcessor: 0             
        UserTime                  00:00:00.015
        KernelTime                00:00:00.000
        Win32 Start Address 0x00007ff7fb928de0
        Stack Init ffffd001c2ec6dd0 Current ffffd001c2ec60c0
        Base ffffd001c2ec7000 Limit ffffd001c2ec1000 Call 0
        Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
        Kernel stack not resident.

        THREAD ffffe001d115c080  Cid 10f0.15b4  Teb: 000000ee6cf9b000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d0bf0640  QueueObject
        Not impersonating
        DeviceMap                 ffffc00019113080
        Owning Process            ffffe001d147c840       Image:         audiodg.exe
        Attached Process          N/A            Image:         N/A
        Wait Start TickCount      338852         Ticks: 197682 (0:00:51:28.781)
        Context Switch Count      1              IdealProcessor: 0             
        UserTime                  00:00:00.000
        KernelTime                00:00:00.000
        Win32 Start Address 0x00007fff6978b350
        Stack Init ffffd001c3143dd0 Current ffffd001c3143520
        Base ffffd001c3144000 Limit ffffd001c313e000 Call 0
        Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
        Kernel stack not resident.

        THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 WAIT: (WrQueue) UserMode Alertable
            ffffe001d173e5c0  QueueObject
        Not impersonating
        DeviceMap                 ffffc00019113080
        Owning Process            ffffe001d147c840       Image:         audiodg.exe
        Attached Process          N/A            Image:         N/A
        Wait Start TickCount      518918         Ticks: 17616 (0:00:04:35.250)
        Context Switch Count      9              IdealProcessor: 1             
        UserTime                  00:00:00.000
        KernelTime                00:00:00.000
        Win32 Start Address 0x00007fff6978b350
        Stack Init ffffd001c70c6dd0 Current ffffd001c70c6520
        Base ffffd001c70c7000 Limit ffffd001c70c1000 Call 0
        Priority 9 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
        Kernel stack not resident.
```

此代码未处于活动状态，因为所有的线程处于等待状态，按预期方式。

**线程**

若要查看和设置线程的命令是非常类似于那些进程。 使用[ **！ 线程**](-thread.md)命令查看线程。 使用[ **.thread** ](-thread--set-register-context-.md)设置当前线程。

若要浏览使用 media player 相关联的线程，请再次播放媒体剪辑。 如果在上一部分中所述的断点仍然存在，你可以停止 audiodg.exe 的上下文中。

使用 ！ 线程为-1 0 若要显示当前线程的信息摘要。 这将显示地址、 线程和进程 Id、 线程环境块 (TEB) 地址，该线程的 Win32 函数 （如果有） 的地址已创建线程运行，然后在线程计划状态。

```dbgcmd
0: kd> !thread -1 0
THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 RUNNING on processor 0
```

若要查看有关正在运行的线程的详细信息，请键入[ **！ 线程**](-thread.md)。 应显示类似于以下的信息。

```dbgcmd
0: kd> !thread
THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 RUNNING on processor 0
IRP List:
    ffffe001d429e580: (0006,02c8) Flags: 000008b4  Mdl: 00000000
Not impersonating
DeviceMap                 ffffc00019113080
Owning Process            ffffe001d147c840       Image:         audiodg.exe
Attached Process          N/A            Image:         N/A
Wait Start TickCount      537630         Ticks: 0
Context Switch Count      63             IdealProcessor: 1             
UserTime                  00:00:00.000
KernelTime                00:00:00.015
Win32 Start Address 0x00007fff6978b350
Stack Init ffffd001c70c6dd0 Current ffffd001c70c6520
Base ffffd001c70c7000 Limit ffffd001c70c1000 Call 0
Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
Child-SP          RetAddr           : Args to Child                                                           : Call Site
ffffd001`c70c62a8 fffff800`7a0fa607 : ffffe001`d4aec5c0 ffffe001`cdefd3d8 ffffe001`d4aec5c0 ffffe001`cdefd390 : tabletaudiosample!CMiniportWaveRT::NewStream [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 562]
ffffd001`c70c62b0 fffff800`7a0fb2c3 : 00000000`00000000 ffffe001`d429e580 ffffe001`d4ea47b0 ffffe001`cdefd3d8 : portcls!CPortPinWaveRT::Init+0x2e7
ffffd001`c70c6340 fffff800`7a0fc7f9 : ffffe001`d4aec430 00000000`00000000 ffffe001`d10b8380 ffffe001`d429e580 : portcls!CPortFilterWaveRT::NewIrpTarget+0x193
ffffd001`c70c63c0 fffff800`7a180552 : 00000000`00000000 ffffe001`d10b8380 ffffe001`d429e580 ffffe001`d4565600 : portcls!xDispatchCreate+0xd9
ffffd001`c70c6450 fffff800`7a109a9a : ffffe001`d10b84d0 ffffe001`d10b8380 00000000`00000000 ffffe001`00000000 : ks!KsDispatchIrp+0x272
ffffd001`c70c6510 fffff800`7bd314b1 : ffffe001`d429e580 ffffd001`c70c6590 ffffe001`d429e800 ffffe001`ce80da70 : portcls!DispatchCreate+0x7a
ffffd001`c70c6540 fffff803`cda1bfa8 : 00000000`00000025 00000000`00000000 00000000`00000000 ffffe001`d429e580 : ksthunk!CKernelFilterDevice::DispatchIrp+0xf9
ffffd001`c70c65a0 fffff803`cda7b306 : 00000000`000002fc ffffe001`d5e0d510 00000000`00000000 ffffe001`d3341bd0 : nt!IopParseDevice+0x7c8
ffffd001`c70c6770 fffff803`cda12916 : 00000000`000002fc ffffd001`c70c68d0 ffffe001`d3341ba0 fffff803`cda7b250 : nt!IopParseFile+0xb6
ffffd001`c70c67d0 fffff803`cda1131c : ffffe001`ceb6c601 ffffd001`c70c69e0 00000000`00000040 ffffe001`cd127dc0 : nt!ObpLookupObjectName+0x776
ffffd001`c70c6970 fffff803`cd9fedb8 : ffff8ab8`00000001 ffffe001`d5e0d510 00000000`00000000 00000000`00000000 : nt!ObOpenObjectByNameEx+0x1ec
ffffd001`c70c6a90 fffff803`cd9fe919 : 000000ee`6d37c6e8 00000004`6d37c500 000000ee`6d37c5f0 000000ee`6d37c5e0 : nt!IopCreateFile+0x3d8
ffffd001`c70c6b40 fffff803`cd752fa3 : fffff6fb`7da05360 fffff6fb`40a6c0a8 fffff681`4d815760 ffff8ab8`92895e23 : nt!NtCreateFile+0x79
ffffd001`c70c6bd0 00007fff`69805b74 : 00007fff`487484e6 0000029b`00000003 00000000`0000012e 00000000`00000000 : nt!KiSystemServiceCopyEnd+0x13 (TrapFrame @ ffffd001`c70c6c40)
000000ee`6d37c568 00007fff`487484e6 : 0000029b`00000003 00000000`0000012e 00000000`00000000 00000000`00000000 : 0x00007fff`69805b74
000000ee`6d37c570 0000029b`00000003 : 00000000`0000012e 00000000`00000000 00000000`00000000 00000000`00000000 : 0x00007fff`487484e6
000000ee`6d37c578 00000000`0000012e : 00000000`00000000 00000000`00000000 00000000`00000000 00000000`00000080 : 0x0000029b`00000003
000000ee`6d37c580 00000000`00000000 : 00000000`00000000 00000000`00000000 00000000`00000080 00000000`00000000 : 0x12e
```

使用 k 命令来查看调用堆栈与线程关联。

```dbgcmd
0: kd> k
# Child-SP          RetAddr           Call Site
00 ffffd001`c70c62a8 fffff800`7a0fa607 tabletaudiosample!CMiniportWaveRT::NewStream [c:\data1\threshold\audio\endpointscommon\minwavert.cpp @ 562]
01 ffffd001`c70c62b0 fffff800`7a0fb2c3 portcls!CPortPinWaveRT::Init+0x2e7
02 ffffd001`c70c6340 fffff800`7a0fc7f9 portcls!CPortFilterWaveRT::NewIrpTarget+0x193
03 ffffd001`c70c63c0 fffff800`7a180552 portcls!xDispatchCreate+0xd9
04 ffffd001`c70c6450 fffff800`7a109a9a ks!KsDispatchIrp+0x272
05 ffffd001`c70c6510 fffff800`7bd314b1 portcls!DispatchCreate+0x7a
06 ffffd001`c70c6540 fffff803`cda1bfa8 ksthunk!CKernelFilterDevice::DispatchIrp+0xf9
07 ffffd001`c70c65a0 fffff803`cda7b306 nt!IopParseDevice+0x7c8
08 ffffd001`c70c6770 fffff803`cda12916 nt!IopParseFile+0xb6
09 ffffd001`c70c67d0 fffff803`cda1131c nt!ObpLookupObjectName+0x776
0a ffffd001`c70c6970 fffff803`cd9fedb8 nt!ObOpenObjectByNameEx+0x1ec
0b ffffd001`c70c6a90 fffff803`cd9fe919 nt!IopCreateFile+0x3d8
0c ffffd001`c70c6b40 fffff803`cd752fa3 nt!NtCreateFile+0x79
0d ffffd001`c70c6bd0 00007fff`69805b74 nt!KiSystemServiceCopyEnd+0x13
0e 000000ee`6d37c568 00007fff`487484e6 0x00007fff`69805b74
0f 000000ee`6d37c570 0000029b`00000003 0x00007fff`487484e6
10 000000ee`6d37c578 00000000`0000012e 0x0000029b`00000003
11 000000ee`6d37c580 00000000`00000000 0x12e
```

输入 g 到调试器中运行代码前滚直到完成媒体剪辑播放。 然后到调试器中断通过按 Ctrl-ScrLk (ctrl + Break) 使用 ！ thread 命令以确认现在运行不同的线程。

```dbgcmd
0: kd> !thread
THREAD ffffe001ce80b840  Cid 17e4.01ec  Teb: 00000071fa9b9000 Win32Thread: ffffe001d41690d0 RUNNING on processor 0
Not impersonating
DeviceMap                 ffffc0001974e2c0
Owning Process            ffffe001d1760840       Image:         rundll32.exe
Attached Process          N/A            Image:         N/A
Wait Start TickCount      538040         Ticks: 0
Context Switch Count      3181840        IdealProcessor: 0             
UserTime                  00:00:08.250
KernelTime                00:00:10.796
Win32 Start Address 0x00007ff6d2f24270
Stack Init ffffd001cd16afd0 Current ffffd001cd16a730
Base ffffd001cd16b000 Limit ffffd001cd165000 Call 0
Priority 8 BasePriority 8 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5

Child-SP          RetAddr           : Args to Child                                                           : Call Site
fffff803`cf373d18 fffff800`7a202852 : fffff803`cf373e60 00000000`00000001 ffffe001`cf4ed330 00000000`0000ffff : nt!DbgBreakPointWithStatus
fffff803`cf373d20 fffff803`cd6742c6 : ffffe001`cf4ed2f0 fffff803`cf373e60 00000000`00000001 00000000`0004e4b8 : kdnic!TXSendCompleteDpc+0x142
fffff803`cf373d60 fffff803`cd74d495 : 00000000`00000000 fffff803`cd923180 fffff803`cde1f4b0 fffff901`40669010 : nt!KiRetireDpcList+0x5f6
fffff803`cf373fb0 fffff803`cd74d2a0 : 00000000`00000090 0000000e`0000006a 00000000`00000092 00000000`00000000 : nt!KxRetireDpcList+0x5 (TrapFrame @ fffff803`cf373e70)
ffffd001`cd16a6c0 fffff803`cd74bd75 : 00000000`00000000 fffff803`cd74a031 00000000`00000000 00000000`00000000 : nt!KiDispatchInterruptContinue
ffffd001`cd16a6f0 fffff803`cd74a031 : 00000000`00000000 00000000`00000000 ffffe001`cff4d2a0 fffff803`cd67738e : nt!KiDpcInterruptBypass+0x25
ffffd001`cd16a700 fffff960`50cdb5a4 : fffff901`400006d0 00000000`00000001 fffff901`40000d60 ffffd001`cd16a9f0 : nt!KiInterruptDispatchNoLockNoEtw+0xb1 (TrapFrame @ ffffd001`cd16a700)
ffffd001`cd16a890 fffff960`50c66b2f : 00000000`00000000 fffff901`40669010 fffff901`42358580 fffff901`40000d60 : win32kfull!Win32FreePoolImpl+0x34
ffffd001`cd16a8c0 fffff960`50c68cd6 : 00000000`00000000 ffffd001`cd16a9f0 fffff901`400006d0 fffff901`400c0460 : win32kfull!EXLATEOBJ::vAltUnlock+0x1f
ffffd001`cd16a8f0 fffff803`cd752fa3 : 00000000`00000000 00000000`00000000 ffffe001`ce80b840 00000000`00000000 : win32kfull!NtGdiAlphaBlend+0x1d16
ffffd001`cd16add0 00007fff`674c1494 : 00007fff`674b1e97 0000a7c6`daee0559 00000000`00000001 0000020b`741f3c50 : nt!KiSystemServiceCopyEnd+0x13 (TrapFrame @ ffffd001`cd16ae40)
00000071`fa74c9a8 00007fff`674b1e97 : 0000a7c6`daee0559 00000000`00000001 0000020b`741f3c50 00000000`00ffffff : 0x00007fff`674c1494
00000071`fa74c9b0 0000a7c6`daee0559 : 00000000`00000001 0000020b`741f3c50 00000000`00ffffff 00000000`00000030 : 0x00007fff`674b1e97
00000071`fa74c9b8 00000000`00000001 : 0000020b`741f3c50 00000000`00ffffff 00000000`00000030 00000000`01010bff : 0x0000a7c6`daee0559
00000071`fa74c9c0 0000020b`741f3c50 : 00000000`00ffffff 00000000`00000030 00000000`01010bff 00000000`00000000 : 0x1
00000071`fa74c9c8 00000000`00ffffff : 00000000`00000030 00000000`01010bff 00000000`00000000 00000000`000000c0 : 0x0000020b`741f3c50
00000071`fa74c9d0 00000000`00000030 : 00000000`01010bff 00000000`00000000 00000000`000000c0 00000000`00000030 : 0xffffff
00000071`fa74c9d8 00000000`01010bff : 00000000`00000000 00000000`000000c0 00000000`00000030 00000071`00000030 : 0x30
00000071`fa74c9e0 00000000`00000000 : 00000000`000000c0 00000000`00000030 00000071`00000030 00000071`01ff8000 : 0x1010bff
```

映像名称是 rundll32.exe，它确实不与播放媒体剪辑相关联的映像名称。

**请注意**  若要设置当前线程，请键入.thread&lt;线程号&gt;。

有关线程和进程的详细信息，请参阅以下引用：

[线程和进程](threads-and-processes.md)

[更改上下文](changing-contexts.md)

 

## <a name="span-idirqlregistersmemoryspansection-11-irql-registers-and-disassembly"></a><span id="irqlregistersmemory"></span>第 11 节：IRQL、 寄存器和反汇编


### <a name="span-idviewthesavedirqlspanview-the-saved-irql"></a><span id="view_the_saved_irql"></span>查看已保存的 IRQL

*在第 11 节，将显示 irql，因此和 regsisters 的内容。*

**&lt;在主机系统**

中断请求级别 (IRQL) 用于管理的服务中断的优先级。 每个处理器都有线程可以提高或降低的 IRQL 设置。 中断的发生或以下处理器的 IRQL 设置被屏蔽并不会干扰当前操作。 中断的发生以上处理器的 IRQL 设置优先于当前操作。 [ **！ Irql** ](-irql.md)扩展当前的目标计算机的处理器上显示的中断请求级别 (IRQL)，在调试器中断发生之前。 当目标计算机进入调试器，IRQL 更改，但 IRQL 有效只是随着在调试器中断保存和显示通过 ！ irql。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanview-the-registers-and-disassembly"></a><<span id="viewingtheregisters"></span>查看寄存器和反汇编

**查看注册**

使用当前处理器上显示当前线程的寄存器的内容[ **r （寄存器）** ](r--registers-.md)命令。

```dbgcmd
0: kd> r
rax=000000000000c301 rbx=ffffe00173eed880 rcx=0000000000000001
rdx=000000d800000000 rsi=ffffe00173eed8e0 rdi=ffffe00173eed8f0
rip=fffff803bb757020 rsp=ffffd001f01f8988 rbp=ffffe00173f0b620
 r8=000000000000003e  r9=ffffe00167a4a000 r10=000000000000001e
r11=ffffd001f01f88f8 r12=0000000000000000 r13=ffffd001f01efdc0
r14=0000000000000001 r15=0000000000000000
iopl=0         nv up ei pl nz na pe nc
cs=0010  ss=0018  ds=002b  es=002b  fs=0053  gs=002b             efl=00000202
nt!DbgBreakPointWithStatus:
fffff803`bb757020 cc              int     3
```

或者，您可以通过单击显示寄存器的内容**视图** &gt; **注册**。

![windbg 寄存器窗口显示 12 个寄存器](images/sysvad-lab-audio-display-registers.png)

逐句通过程序集语言代码执行和在其他情况下时，查看寄存器内容非常有用。 有关详细信息请参阅[ **r （寄存器）**](r--registers-.md)。

寄存器的内容的信息，请参阅[x86 体系结构](x86-architecture.md)并[x64 体系结构](x64-architecture.md)。

**反汇编**

可以反汇编正在执行可以查看通过单击正在运行的程序集语言代码的代码**视图** &gt; **反汇编**。

![windbg 反汇编窗口](images/sysvad-lab-audio-disassembly-window.png)

有关程序集语言反汇编的详细信息，请参阅[Annotated x86 反汇编](annotated-x86-disassembly.md)并[Annotated x64 反汇编](annotated-x64-disassembly.md)。

## <a name="span-idworkingwithmemoryspansection-12-work-with-memory"></a><span id="workingwithmemory"></span>第 12 节：使用内存


*在部分 12 中，将使用调试器命令以显示内存中的内容。*

**查看内存**

您可能需要检查以确定问题，或若要检查变量、 指针和等等的内存。 可以通过键入以下项之一来显示内存**d\* &lt;地址&gt;** 命令。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>db</p></td>
<td align="left"><p>字节值和 ASCII 字符中显示数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dd</p></td>
<td align="left"><p>数据显示为双精度宽单词 （4 个字节为单位）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>du</p></td>
<td align="left"><p>数据显示为 Unicode 字符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dw</p></td>
<td align="left"><p>数据显示为字值 （2 个字节） 和 ASCII 字符。</p></td>
</tr>
</tbody>
</table>

 

**请注意**  如果您试图显示无效的地址，其内容如下所示的问号 （？）。

 

或者，可以通过单击查看内存**视图** &gt; **内存**。 使用**显示格式**展开下拉列表来更改显示内存的方式。

![windbg 视图内存窗口](images/sysvad-lab-audio-memory-display.png)

1.  若要查看与音量控件关联的数据，设置断点，以使用 bm 命令 PropertyHandlerAudioEngineVolumeLevel 例程上激发。 我们将设置新断点之前，我们将清除所有使用 bc 的上一个断点\*。

    ```dbgcmd
    kd> bc *
    ```

2.  设置断点，以使用 bm 命令 PropertyHandlerAudioEngineVolumeLevel 例程上激发。

    ```dbgcmd
    kd> bm tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

3.  列出要确认正确设置了断点的断点。

    ```dbgcmd
    kd> bl
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

4.  使用**g**命令来重新启动代码执行。

    在目标系统上调整系统任务栏中的卷。 这将导致触发断点。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume:
    fffff80f`02c3a4b0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

5.  使用**视图**&gt; **本地**菜单项以显示本地变量。 请注意 IVolume 变量的当前值。

6.  您可以显示的数据类型和 IVolume 变量的当前值的示例代码中通过键入**dt**命令和变量的名称。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xa011ea50 Type long
    0n-6291456
    ```

7.  输入 SetDeviceChannelVolume 便会命中断点。

    ```dbgcmd
    STDMETHODIMP_(NTSTATUS) CMiniportWaveRT::SetDeviceChannelVolume(_In_  ULONG _ulNodeId, _In_ UINT32 _uiChannel, _In_  LONG  _Volume)
    {
        NTSTATUS ntStatus = STATUS_INVALID_DEVICE_REQUEST;

        PAGED_CODE ();

        DPF_ENTER(("[CMiniportWaveRT::SetEndpointChannelVolume]"));
        IF_TRUE_ACTION_JUMP(_ulNodeId != KSNODE_WAVE_AUDIO_ENGINE, ntStatus = STATUS_INVALID_DEVICE_REQUEST, Exit);

        // Snap the volume level to our range of steppings.
        LONG lVolume = VOLUME_NORMALIZE_IN_RANGE(_Volume); 

        ntStatus = SetChannelVolume(_uiChannel, lVolume);
    Exit:
        return ntStatus;
    }
    ```

8.  尝试使用 IVolume 的内存位置显示值[ **dt （显示类型）** ](dt--display-type-.md)命令。

    ```dbgcmd
    kd> dt dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n0
    ```

    因为变量尚未定义，所以它不包含的信息。

9.  按 F10 以转发到最后一个代码行中运行 SetDeviceChannelVolume。

    ```dbgcmd
        return ntStatus;
    ```

10. 通过使用 IVolume 的内存位置显示的值[ **dt （显示类型）** ](dt--display-type-.md)命令。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n-6291456
    ```

    现在，该变量处于活动状态，在此示例中显示的 6291456 值。

11. 此外可以通过使用显示的内存位置的 IVolume [ **？（计算表达式）** ](---evaluate-expression-.md)命令。

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

12. 所示，地址*ffffb780\`b7eee664*是 lVolume 变量的地址。 Dd 命令用于在该位置显示内存中的内容。

    ```dbgcmd
    kd>  dd ffffb780`b7eee664
    ffffb780`b7eee664  ffa00000 00000018 00000000 c52d7008
    ffffb780`b7eee674  ffffc98e e0495756 fffff80e c52d7008
    ffffb780`b7eee684  ffffc98e 00000000 fffff80e 00000000
    ffffb780`b7eee694  ffffc98e ffa00000 ffffb780 b7eee710
    ffffb780`b7eee6a4  ffffb780 00000000 00000000 c7477260
    ffffb780`b7eee6b4  ffffc98e b7eee7a0 ffffb780 b7eee6f0
    ffffb780`b7eee6c4  ffffb780 e04959ca fffff80e 00000000
    ffffb780`b7eee6d4  00000000 00000028 00000000 00000002
    ```

13. 可以通过指定范围参数 L4 显示地址的前四个字节。

    ```dbgcmd
    kd> dd ffffb780`b7eee664 l4
    ffffb780`b7eee664  ffa00000 00000018 00000000 c52d7008
    ```

14. 若要查看不同类型的内存输出显示，请键入**du**， **da**并**db**命令。

    ```dbgcmd
    kd> du ffffb780`b7eee664 
    ffffb780`b7eee664  ""

    kd> a ffffb780`b7eee664 
    ffffb780`b7eee664  ""

    kd> db 0xffffae015ff97664 
    ffffae01`5ff97664  00 80 bc ff 18 00 00 00-00 00 00 00 08 50 e0 51  .............P.Q
    ffffae01`5ff97674  00 c0 ff ff 56 57 da 56-0e f8 ff ff 08 50 e0 51  ....VW.V.....P.Q
    ffffae01`5ff97684  00 c0 ff ff 00 00 00 00-0e f8 ff ff 00 00 00 00  ................
    ffffae01`5ff97694  00 c0 ff ff aa 80 bc ff-01 ae ff ff 10 77 f9 5f  .............w._
    ffffae01`5ff976a4  01 ae ff ff 40 00 00 00-00 e6 ff ff 10 dc 30 55  ....@.........0U
    ffffae01`5ff976b4  00 c0 ff ff a0 77 f9 5f-01 ae ff ff f0 76 f9 5f  .....w._.....v._
    ffffae01`5ff976c4  01 ae ff ff ca 59 da 56-0e f8 ff ff 00 00 00 00  .....Y.V........
    ffffae01`5ff976d4  00 00 00 00 28 00 00 00-00 00 00 00 02 00 00 00  ....(...........
    ```

    Df float 选项用于将数据显示为单精度浮点数 （4 个字节为单位）。

    ```dbgcmd
    df ffffb780`b7eee664 
    ffffb780`b7eee664          -1.#QNAN   3.3631163e-044                0        -2775.002
    ffffb780`b7eee674          -1.#QNAN  -5.8032637e+019         -1.#QNAN        -2775.002
    ffffb780`b7eee684          -1.#QNAN                0         -1.#QNAN                0
    ffffb780`b7eee694          -1.#QNAN         -1.#QNAN         -1.#QNAN  -2.8479408e-005
    ```

**写入内存**

类似于用来读取内存的命令，可以使用电子\*命令来更改内存内容。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ea</p></td>
<td align="left"><p>ASCII 字符串 （不以 NULL 终止）</p></td>
</tr>
<tr class="even">
<td align="left"><p>欧盟</p></td>
<td align="left"><p>（不以 NULL 终止的 Unicode 字符串</p></td>
</tr>
<tr class="odd">
<td align="left"><p>新增功能</p></td>
<td align="left"><p>字值 （2 个字节）</p></td>
</tr>
<tr class="even">
<td align="left"><p>eza</p></td>
<td align="left"><p>以 NULL 结尾的 ASCII 字符串</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ezu</p></td>
<td align="left"><p>NULL 终止的 Unicode 字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p>eb</p></td>
<td align="left"><p>字节值</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ed</p></td>
<td align="left"><p>双字值 （4 字节）</p></td>
</tr>
</tbody>
</table>

 

下面的示例演示如何覆盖内存。

1.  首先，在示例代码中找到使用 lVolume 的地址。

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

2.  使用新字符使用覆盖该内存地址**eb**命令。

    ```dbgcmd
    kd> eb 0xffffb780`b7eee664 11 11 11 11 11
    ```

3.  显示内存位置，若要确认已被字符覆盖通过键入**db**命令。

    ```dbgcmd
    kd> db 0xffffb780`b7eee664
    ffffb780`b7eee664  11 11 11 11 11 00 00 00-00 00 00 00 08 70 2d c5  .............p-.
    ffffb780`b7eee674  8e c9 ff ff 56 57 49 e0-0e f8 ff ff 08 70 2d c5  ....VWI......p-.
    ffffb780`b7eee684  8e c9 ff ff 00 00 00 00-0e f8 ff ff 00 00 00 00  ................
    ffffb780`b7eee694  8e c9 ff ff 00 00 a0 ff-80 b7 ff ff 10 e7 ee b7  ................
    ffffb780`b7eee6a4  80 b7 ff ff 00 00 00 00-00 00 00 00 60 72 47 c7  ............`rG.
    ffffb780`b7eee6b4  8e c9 ff ff a0 e7 ee b7-80 b7 ff ff f0 e6 ee b7  ................
    ffffb780`b7eee6c4  80 b7 ff ff ca 59 49 e0-0e f8 ff ff 00 00 00 00  .....YI.........
    ffffb780`b7eee6d4  00 00 00 00 28 00 00 00-00 00 00 00 02 00 00 00  ....(...........
    ```

或者，您可以修改的监视或局部变量窗口中的内存的内容。 对于监视窗口中，可能会看到超出当前帧的上下文的变量。 不相关，如果它们不在上下文中对其进行修改。

## <a name="span-idendingthesessionspansection-13-end-the-windbg-session"></a><span id="endingthesession"></span>第 13 节：结束 WinDbg 会话


**&lt;在主机系统**

若要用户模式下调试会话结束，返回休眠模式下，调试器并设置目标应用程序再次运行，请输入**qd** （Quit 和分离） 命令。

确保并用**g**命令，以使目标计算机运行的代码，以便可以使用它。 它还建议清除任何断点，使用 * * bc \\* * *，以便目标计算机不会中断并尝试连接到主机计算机调试器。

```dbgcmd
0: kd> qd
```

有关详细信息，请参阅[结束调试会话在 WinDbg 中](ending-a-debugging-session-in-windbg.md)调试的参考文档中。

## <a name="span-idwindowsdebuggingresourcesspansection-14-windows-debugging-resources"></a><span id="windowsdebuggingresources"></span>第 14 节：Windows 调试资源


有关 Windows 调试提供了其他信息。 请注意，这些书籍将使用在其示例中，如 Windows Vista 的 Windows 的较旧版本，但要讨论的概念也适用于大多数版本的 Windows。

**丛书**

-   *高级 Windows 调试*Mario Hewardt 和 Daniel Pravat

-   *深入了解 Windows 调试：调试和跟踪策略 Windows® 中的实用指南*通过 Tarik Soulami

-   *Windows 内部结构*Mark E.Russinovich、 David A.Solomon 和 Alex Ionescu

**视频**

碎片整理工具显示 WinDbg 剧集 13 29 <https://channel9.msdn.com/Shows/Defrag-Tools>

**培训供应商：**

OSR  - <https://www.osr.com/>


## <a name="see-also"></a>请参阅

[Windows 调试入门](getting-started-with-windows-debugging.md) 

 





