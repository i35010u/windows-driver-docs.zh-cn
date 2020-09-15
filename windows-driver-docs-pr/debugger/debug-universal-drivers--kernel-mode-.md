---
title: '调试驱动程序-分步实验室 (Sysvad 内核模式) '
description: 此实验室提供练习，演示如何调试 Sysvad 音频内核模式设备驱动程序。
ms.assetid: 4A31451C-FC7E-4C5F-B4EB-FBBAC8DADF9E
keywords:
- 调试实验室
- 循序渐进
- SYSVAD
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: fd2b5b9e83611bb757930615e078e9a49ba9eaa3
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90107006"
---
# <a name="span-iddebuggerdebug_universal_drivers__kernel-mode_spandebug-drivers---step-by-step-lab-sysvad-kernel-mode"></a><span id="debugger.debug_universal_drivers__kernel-mode_"></span>调试驱动程序-逐步骤实验室 (Sysvad 内核模式) 

此实验室提供练习，演示如何调试 Sysvad 音频内核模式设备驱动程序。

Microsoft Windows 调试器 (WinDbg) 是一个功能强大的基于 Windows 的调试工具，可用于执行用户模式和内核模式调试。 WinDbg 为 Windows 内核、内核模式驱动程序和系统服务以及用户模式应用程序和驱动程序提供源级调试。

WinDbg 可以单步执行源代码、设置断点、查看变量 (包括 c + + 对象) 、堆栈跟踪和内存。 它的调试器命令窗口允许用户发出多种命令。

## <a name="span-idlab_setupspanlab-setup"></a><span id="lab_setup"></span>实验室设置

你将需要以下硬件才能完成实验室：

-   运行 Windows 10 (主机) 的便携式计算机或台式计算机
-   运行 Windows 10 (目标) 的便携式计算机或台式计算机
-   用于连接两台电脑的网络集线器/路由器和网络电缆
-   访问 internet 以下载符号文件

你将需要以下软件才能完成实验室。

-   Microsoft Visual Studio 2017
-   适用于 Windows 10 的 Windows 软件开发工具包 (SDK)
-   适用于 Windows 10 的 windows 驱动程序工具包 (WDK) 
-   适用于 Windows 10 的示例 Sysvad 音频驱动程序

有关下载和安装 WDK 的信息，请参阅 [ (WDK) 下载 Windows 驱动程序工具包 ](../download-the-wdk.md)。

## <a name="span-idsysvad_debugging_walkthrough_overviewspansysvad-debugging-walkthrough"></a><span id="sysvad_debugging_walkthrough_overview"></span>Sysvad 调试演练


此实验室将引导你完成调试内核模式驱动程序的过程。 练习使用 Syvad 虚拟音频驱动程序示例。 由于 Syvad 音频驱动程序与实际音频硬件不交互，因此它可以在大多数设备上使用。 实验室涉及以下任务：

-   [第1节：连接到内核模式 WinDbg 会话](#connectto)
-   [第2部分：内核模式调试命令和技术](#kernelmodedebuggingcommandsandtechniques)
-   [第3部分：下载并构建 Sysvad 音频驱动程序](#download)
-   [第4部分：在目标系统上安装 Sysvad 音频驱动程序](#install)
-   [第5节：使用 WinDbg 显示有关驱动程序的信息](#usewindbgtodisplayinformation)
-   [第6部分：显示即插即用设备树信息](#displayingtheplugandplaydevicetree)
-   [第7部分：处理断点和源代码](#workingwithbreakpoints)
-   [第8节：查看变量](#lookingatvariables)
-   [第9节：查看调用堆栈](#viewingcallstacks)
-   [第10部分：显示进程和线程](#displayingprocessesandthreads)
-   [第11节： IRQL、寄存器和反汇编](#irqlregistersmemory)
-   [第12部分：使用内存](#workingwithmemory)
-   [第13部分：结束 WinDbg 会话](#endingthesession)
-   [第14节： Windows 调试资源](#windowsdebuggingresources)

## <a name="span-idecho_driver_labspanecho-driver-lab"></a><span id="echo_driver_lab"></span>回显驱动程序实验室


回显驱动程序是一个更简单的驱动程序，然后是 Sysvad 音频驱动程序。 如果你不熟悉 WinDbg，可能需要考虑首先完成 [调试通用驱动程序-分步实验室 (Echo 内核模式) ](debug-universal-drivers---step-by-step-lab--echo-kernel-mode-.md)。 此实验室重用该实验室的安装方向，因此，如果完成了该实验，则可以跳过此处的第1和第2部分。

## <a name="span-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span>第1节：连接到内核模式 WinDbg 会话


*在第1部分中，你将在主机和目标系统上配置网络调试。*

此实验室中的电脑需要配置为使用以太网网络连接进行内核调试。

此实验室使用两台计算机。 WinDbg 在 *主机* 系统上运行，Sysvad 驱动程序在 *目标* 系统上运行。

 使用网络集线器/路由器和网络电缆连接两台 Pc。

![使用双箭头连接的两台电脑](images/debuglab-image-targethostdrawing1.png)

若要使用内核模式应用程序并使用 WinDbg，建议使用 KDNET over 以太网传输。 有关如何使用以太网传输协议的信息，请参阅 [使用 WinDbg (内核模式) 入门 ](getting-started-with-windbg--kernel-mode-.md)。 有关设置目标计算机的详细信息，请参阅 [为手动驱动程序部署准备计算机](/windows-hardware/drivers) 和 [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

### <a name="span-idconfigure__kernel_mode_debugging_using_ethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="configure__kernel_mode_debugging_using_ethernet"></span>使用以太网配置内核-模式调试

若要在目标系统上启用内核模式调试，请执行以下步骤。

**&lt;-在主机系统上**

1. 在主机系统上打开命令提示符，然后键入 **ipconfig/all** 来确定其 IP 地址。

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

3. 记录主机系统的主机名： \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**-&gt; 在目标系统上**

4. 在目标系统上打开命令提示符，并使用 **ping** 命令确认两个系统之间的网络连接。 使用所记录主机系统的实际 IP 地址，而不是示例输出中所示的169.182.1.1。

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

若要使用 KDNET 实用程序在目标系统上启用内核模式调试，请执行以下步骤。

1. 在主机系统上，找到 WDK KDNET 目录。 默认情况下，它位于此处。

   C:\Program 文件 (x86) \Windows Kits\10\Debuggers\x64

> [!NOTE]
> 此实验假设两台 Pc 同时运行 Windowson 的64位版本的。 如果不是这种情况，最好的方法是在目标正在运行的主机上运行相同的工具 "位数"。 例如，如果目标运行的是32位 Windows，请在主机上运行调试器的32版本。 有关详细信息，请参阅 [选择32位或64位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
> 

2. 找到这两个文件，并将它们复制到网络共享或拇指驱动器上，以便它们将在目标计算机上可用。

    kdnet.exe

    VerifiedNICList.xml


3. 在目标计算机上，以管理员身份打开“命令提示符”窗口。 输入此命令以验证目标 PC 上的 NIC 是否支持。

```console
C:\KDNET>kdnet

Network debugging is supported on the following NICs:
busparams=0.25.0, Intel(R) 82579LM Gigabit Network Connection, KDNET is running on this NIC.kdnet.exe
```

4. 键入此命令可设置主机系统的 IP 地址。 使用所记录主机系统的实际 IP 地址，而不是示例输出中所示的169.182.1.1。 为使用的每个目标/主机对（如50010）选择唯一的端口地址。

```console
C:\>kdnet 169.182.1.1 50010

Enabling network debugging on Intel(R) 82577LM Gigabit Network Connection.
Key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。
>

5. 键入以下命令以确认 dbgsettings 设置正确。

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

将自动生成的唯一键复制到文本文件中，以避免在主机 PC 上键入。 将带有密钥的文本文件复制到主机系统。

**注意**   
**防火墙和调试器**

如果收到来自防火墙的弹出消息，并且想要使用调试器，请选中 **所有三** 个框。

![windows 安全警报-windows 防火墙阻止了此应用的某些功能](images/debuglab-image-firewall-dialog-box.png)
 

**&lt;-在主机系统上**

1. 在主计算机上，以管理员身份打开命令提示符窗口。 转到 WinDbg.exe 目录。 我们将使用安装 Windows 工具包过程中安装的 Windows 驱动程序工具包 (WDK) 中的 x64 版本 WinDbg.exe。

```console
C:\> Cd C:\Program Files (x86)\Windows Kits\10\Debuggers\x64 
```

2. 使用以下命令通过远程用户调试启动 WinDbg。 密钥和端口的值与前面使用 BCDEdit 在目标上设置的值匹配。

```console
C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
```

**-&gt;在目标系统上**

重新启动目标系统。

**&lt;-在主机系统上**

在一分钟或两分钟内，调试输出应显示在主机系统上。

![显示实时内核连接的命令窗口输出的 windows 调试器](images/debuglab-image-winddbg-hh.png)

调试器命令窗口是 WinDbg 的主调试信息窗口。 您可以在此窗口中输入调试器命令并查看命令输出。

调试器命令窗口拆分为两个窗格。 在窗口底部的 "命令条目" 窗格)  ("命令条目" 窗格中键入命令，然后在窗口顶部的更大窗格中查看命令输出。

在 "命令项" 窗格中，使用向上键和向下键滚动浏览命令历史记录。 显示命令时，你可以对其进行编辑或按 **enter** 运行该命令。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="kernelmodedebuggingcommandsandtechniques"></span>第2部分：内核模式调试命令和技术


*在第2部分中，你将使用 "调试" 命令显示有关目标系统的信息。*

**&lt;-在主机系统上**

**使用 (DML) 启用调试器标记语言。首选 \_ DML**

某些调试命令使用调试器标记语言显示文本，您可以选择该语言来快速收集详细信息。

1. 在 WinDBg 中使用 Ctrl + Break (滚动锁定) ，以中断目标系统上运行的代码。 目标系统可能需要一些时间才能响应。
2. 键入以下命令，在调试器中启用 DML 命令窗口。

```dbgcmd
0: kd> .prefer_dml 1
DML versions of commands on by default
```

**使用 hh 获取帮助**

您可以使用 **hh** 命令访问 reference 命令帮助。

3. 键入以下命令以查看的命令参考帮助 **。首选 \_ dml**。
   ```dbgcmd
   0: kd> .hh .prefer_dml
   ```

调试器帮助文件将显示的帮助 **。 \_ **

![调试器帮助应用程序，显示的帮助。首选 \- dml 命令](images/debuglab-image-prefer-dml-help.png)

**显示目标系统上的 Windows 版本**

5. 通过在 WinDbg 窗口中键入 [**vertarget (显示目标计算机版本) **](vertarget--show-target-computer-version-.md) 命令，在目标系统上显示详细的版本信息。

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

6. 您可以通过在 WinDbg 窗口中键入 " [**lm (List" 已加载的模块) **](lm--list-loaded-modules-.md) "命令来验证是否正在使用正确的内核模式进程。

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

**注意**   已省略的输出用 "...。 "。

 

由于我们尚未设置符号路径和加载的符号，因此在调试器中提供了有限的信息。

## <a name="span-iddownloadspansection-3-download-and-build-the-sysvad-audio-driver"></a><span id="download"></span>第3部分：下载并构建 Sysvad 音频驱动程序


*在第3部分中，你将下载并构建 Sysvad 音频驱动程序。*

通常，使用 WinDbg 时，将使用自己的驱动程序代码。 为了熟悉如何调试音频驱动程序，使用了 Sysvad 虚拟音频示例驱动程序。 此示例用于说明如何单步执行本机内核模式代码。 此方法对于调试复杂的内核模式代码问题非常有用。

若要下载并生成 Sysvad 示例音频驱动程序，请执行以下步骤。

1.  **从 GitHub 下载并提取 Sysvad 音频示例**

    可以使用浏览器在此处查看 Sysvad 示例和 Readme.md 文件：

    [https://github.com/Microsoft/Windows-driver-samples/tree/master/audio/sysvad](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    ![github 存储库显示 "常规文件夹" 和 "下载 zip" 按钮](images/sysvad-lab-github.png)

    此实验室演示如何在一个 zip 文件中下载通用驱动程序示例。

    a. 将 master.zip 文件下载到本地硬盘驱动器。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b. 选择并按住 (或右键单击)  *Windows-driver-samples-master.zip*，然后选择 " **全部提取**"。 指定一个新文件夹，或浏览到将存储所提取文件的现有文件夹。 例如，可以指定*C： \\ WDK \_ 示例 \\ *作为要将文件提取到的新文件夹。

    c. 提取文件后，导航到以下子文件夹。

    *C： \\ WDK \_ 示例 \\ Sysvad*

2.  **在 Visual Studio 中打开驱动程序解决方案**

    在 Visual Studio 中，选择 " **文件**" " &gt; **打开** &gt; **项目/解决方案 ...** "，然后导航到包含提取的文件的文件夹 (例如， *C： \\ WDK \_ Samples \\ Sysvad*) 。 双击 *Syvad* 解决方案文件。

    在 Visual Studio 中找到解决方案资源管理器。  (如果尚未打开，则从 "**视图**" 菜单中选择 "**解决方案资源管理器**"。 ) 解决方案资源管理器中，你可以看到一个具有多个项目的解决方案，并且示例中包含的内容将在不同时间发生变化。 
        
    ![带有从 sysvad 项目加载的设备 .c 文件的 visual studio](images/sysvad-lab-visual-studio-solution.png)

3.  **设置示例的配置和平台**

    在解决方案资源管理器中，选择并按住 (或右键单击) **解决方案 "sysvad" (7 项目) **，然后选择 " **Configuration Manager**"。 请确保这四个项目的配置和平台设置相同。 默认情况下，将配置设置为 "Win10 调试"，并将所有项目的平台设置为 "Win64"。 如果对一个项目进行任何配置和/或平台更改，则必须为其余三个项目进行相同的更改。

    **注意**   此实验室假设正在使用64位 Windows。 如果使用的是32位 Windows，请生成32位的驱动程序。

     

4.  **检查驱动程序签名**

    找到 TabletAudioSample。 打开 Sysvad 驱动程序的属性页，确保将 **驱动程序签名** &gt; **模式** 设置为 " *测试签名*"。

5.  **使用 Visual Studio 生成示例**

    在 Visual Studio 中，选择 " **生成**" "生成 &gt; **解决方案**"。

    生成窗口应显示一条消息，指示已成功生成所有六个项目。

6.  **找到生成的驱动程序文件**

    在 "文件资源管理器" 中，导航到包含示例提取的文件的文件夹。 例如，如果是前面指定的文件夹，请导航到 *C： \\ WDK \_ 示例 \\ Sysvad*。 在该文件夹中，编译的驱动程序文件的位置根据你在 **Configuration Manager**中选择的配置和平台设置而有所不同。 例如，如果将默认设置保持不变，则已编译的驱动程序文件将保存到一个名为* \\ x64 \\ 调试*的名为 "64 位，调试生成" 的文件夹中。

    导航到包含 TabletAudioSample 驱动程序的生成文件的文件夹：

    *C： \\WDK \_ 示例 \\ Sysvad \\ TabletAudioSample \\ x64 \\ 调试*。 文件夹将包含 TabletAudioSample。SYS 驱动程序、符号 pdp 文件和 inf 文件。 还需要查找 SwapAPO 和 KeywordDetectorContosoAdapter dll 和符号文件。

    若要安装该驱动程序，你将需要以下文件。

    | 文件名                         | 说明                                                                       |
    |-----------------------------------|-----------------------------------------------------------------------------------|
    | TabletAudioSample.sys             | 驱动程序文件。                                                                  |
    | TabletAudioSample .pdb             | 驱动程序符号文件。                                                           |
    | tabletaudiosample .inf             |  (INF) 包含安装驱动程序所需的信息的信息。 |
    | KeywordDetectorContosoAdapter  | 示例关键字检测器。                                                        |
    | KeywordDetectorContosoAdapter .pdb | 示例关键字探测器符号文件。                                          |
    | lSwapAPO.dll                      | 用于管理的 UI 的示例驱动程序扩展插件。                                |
    | lSwapAPO .pdb                      | APO UI 符号文件。                                                           |
    | TabletAudioSample .cer             | TabletAudioSample 证书文件。                                           |

     

7.  找到 USB 拇指驱动器或设置网络共享，以将构建的驱动程序文件从主机复制到目标系统。

在下一部分中，你将代码复制到目标系统，然后安装并测试驱动程序。

## <a name="span-idinstallspansection-4-install-the-sysvad-audio-driver-sample-on-the-target-system"></a><span id="install"></span>第4部分：在目标系统上安装 Sysvad 音频驱动程序示例

*在第4部分中，你将使用 devcon 安装 Sysvad 音频驱动程序。*

**-&gt; 在目标系统上**

安装驱动程序的计算机称为 *目标计算机* 或 *测试计算机*。 通常，这是与你开发和构建驱动程序包的计算机不同的计算机。 开发和构建驱动程序的计算机称为 " *主机*"。

将驱动程序包移动到目标计算机并安装驱动程序的过程称为 " *部署* 驱动程序"。

在部署驱动程序之前，必须通过启用测试签名来准备目标计算机。  之后，就可以在目标系统上运行生成的驱动程序示例了。

若要在目标系统上安装驱动程序，请执行以下步骤。

1.  **启用测试签名驱动程序**

    启用运行测试签名驱动程序的功能：

    1. 打开 Windows 设置。

    2. 在 " **更新和安全性**" 中，选择 " **恢复**"。

    3. 在 " **高级启动**" 下，选择 " **立即重新启动**"。

    4. 重新启动计算机后，选择 " **疑难解答**"。

    5. 然后选择 " **高级选项**"、" **启动设置** "，然后选择 " **重新启动**"。

    6. 按 **F7** 键，选择 "禁用驱动程序签名强制"。

    7. 电脑将从新值开始。


3.  **-&gt; 在目标系统上**

    **安装驱动程序**

    下面的说明演示了如何安装和测试示例驱动程序。

    安装此驱动程序所需的 INF 文件为 *TabletAudioSample*。 在目标计算机上，以管理员身份打开“命令提示符”窗口。 导航到 "驱动程序包" 文件夹，右键单击 "TabletAudioSample" 文件，然后选择 " **安装**"。

    此时将显示一个对话框，指示测试驱动程序是未签名驱动程序。 选择“仍然安装此驱动程序”以继续。

    ![windows 安全警告-windows 无法验证发布服务器](images/debuglab-image-install-security-warning.png)

    >[!TIP]
    > 如果安装有任何问题，请查看以下文件以了解详细信息。
    `%windir%\inf\setupapi.dev.log`
    >
     
    有关更多详细说明，请参阅 [配置计算机以进行驱动程序部署、测试和调试](../gettingstarted/provision-a-target-computer-wdk-8-1.md)。

    INF 文件包含用于安装 *tabletaudiosample.sys*的硬件 ID。 对于 Syvad 示例，硬件 ID 为： `root\sysvad_TabletAudioSample`

4.  **查看设备管理器中的驱动程序**

    在目标计算机上的命令提示符窗口中，输入 " **devmgmt.msc** " 以打开设备管理器。 在设备管理器的 "视图" 菜单上，选择 " **设备（按类型**）"。

    在设备树中的 "音频设备" 节点 * (WDM) 中找到 "虚拟音频设备* "。 这通常位于 " **声音、视频和游戏控制器** " 节点下。 确认它已安装并处于活动状态。

    突出显示设备管理器计算机上的实际硬件的驱动程序。 然后选择并按住 (或右键单击该驱动程序) ，然后选择 "禁用" 以禁用该驱动程序。

    确认音频硬件驱动程序设备管理器，并显示向下箭头，指示已将其禁用。

    ![突出显示了虚拟音频设备 tablet 示例的设备管理器树](images/sysvad-lab-audio-device-manager.png)

    成功安装示例驱动程序后，就可以对其进行测试了。

**测试 Sysvad 音频驱动程序**

1. 在目标计算机上的命令提示符窗口中，输入 " **devmgmt.msc** " 以打开设备管理器。 在设备管理器的 " **视图** " 菜单上，选择 " **设备（按类型**）"。 在设备树中，找到 *虚拟音频设备 (WDM) -平板电脑示例*。

2. 打开 "控制面板"，导航到 " **硬件和声音** &gt; **管理音频设备**"。 在 "声音" 对话框中，选择标记为 " *虚拟音频设备 (WDM) -平板电脑*" 的扬声器图标，然后选择 " **设置为默认值**"，但不要选择 **"确定"**。 这会使 "声音" 对话框处于打开状态。
3. 在目标计算机上找到 MP3 或其他音频文件，然后双击以播放该文件。 然后，在 "声音" 对话框中，验证卷级别指示器中是否存在与 *虚拟音频设备 (WDM) -平板电脑示例* 驱动程序相关联的活动。

## <a name="span-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="usewindbgtodisplayinformation"></span>第5节：使用 WinDbg 显示有关驱动程序的信息


*在第5部分中，您将设置符号路径并使用内核调试器命令显示有关 Sysvad 示例驱动程序的信息。*

符号允许 WinDbg 显示其他信息，如变量名称，这在调试时可能非常有用。 WinDbg 使用 Microsoft Visual Studio 调试符号格式进行源级调试。 它可以从包含 PDB 符号文件的模块访问任何符号或变量。

若要加载调试器，请执行以下步骤。

**&lt;-在主机系统上**

1.  如果关闭了调试器，请在管理员命令提示符窗口中使用以下命令重新打开它。 将密钥和端口替换为以前配置的内容。

    ```console
    C:\> WinDbg –k net:port=50010,key=2steg4fzbj2sz.23418vzkd4ko3.1g34ou07z4pev.1sp3yo9yz874p
    ```

2.  使用 Ctrl + Break (滚动锁定) ，以中断目标系统上运行的代码。

**设置符号路径**

1.  若要在 WinDbg 环境中将符号路径设置为 Microsoft 符号服务器，请使用 **symfix** 命令。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  若要添加您的本地符号位置以使用您的本地符号，请使用 **. sympath +** 和 then **/f**添加该路径。

    ```dbgcmd
    0: kd> .sympath+ C:\WDK_Samples\Sysvad
    0: kd> .reload /f
    ```

    **注意**   带有 **/f** force 选项的**reload.sql**命令将删除指定模块的所有符号信息，并重新加载符号。 在某些情况下，此命令还会重新加载或卸载模块本身。

     

**注意**   您必须加载适当的符号才能使用 WinDbg 提供的高级功能。 如果未正确配置符号，则在尝试使用依赖于符号的功能时，你将收到一条消息，指示符号不可用。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```

 

**注意**   
**符号服务器**

有多种方法可用于处理符号。 在许多情况下，可以将 PC 配置为从 Microsoft 在需要时提供的符号服务器访问符号。 本演练假定将使用此方法。 如果你的环境中的符号位于不同的位置，请修改这些步骤以使用该位置。 有关其他信息，请参阅 [符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。

 

**注意**   
**了解源代码符号要求**

若要执行源调试，必须生成已选中 (调试的二进制文件版本) 版本。 编译器将 ( .pdb 文件) 创建符号文件。 这些符号文件将显示调试器与源行的对应关系。 实际的源文件本身还必须可供调试器访问。

符号文件不包含源代码的文本。 对于调试，最好是链接器不优化代码。 如果代码已经过优化，则源调试和对本地变量的访问更难，有时可能几乎不可能。 如果在查看本地变量或源行时遇到问题，请设置以下生成选项。

设置 COMPILE_DEBUG = 1

设置 ENABLE_OPTIMIZER = 0

 

1.  在调试器的 "命令" 区域中键入以下内容以显示有关 Sysvad 驱动程序的信息。

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

    有关详细信息，请参阅 [**lm**](lm--list-loaded-modules-.md)。

2.  选择 "调试输出" 中的 " **浏览所有全局符号** " 链接，以显示以字母 a 开头的项符号的相关信息。
3.  由于已启用 DML，因此输出的某些元素是可供选择的热链接。 选择 "调试输出" 中的 " *数据* " 链接，以显示以字母 a 开头的项符号的相关信息。

    ```dbgcmd
    0: kd> x /D /f tabletaudiosample!a*
     A B C D E F G H I J K L M N O P Q R S T U V W X Y Z

    fffff806`9adb1000 tabletaudiosample!AddDevice (struct _DRIVER_OBJECT *, struct _DEVICE_OBJECT *)
    ```

    有关信息，请参阅 [**x (检查符号) **](x--examine-symbols-.md)。

4.  **！ Lmi**扩展显示有关模块的详细信息。 键入 **！ lmi tabletaudiosample**。 输出应类似于下面所示的文本。

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

5.  使用 **！ dh** 扩展显示标头信息，如下所示。

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

## <a name="span-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="displayingtheplugandplaydevicetree"></span>第6部分：显示即插即用设备树信息


*在第6部分中，将显示有关 Sysvad 示例设备驱动程序以及它在即插即用设备树中的位置的信息。*

有关故障排除的详细信息，请查看即插即用设备树中的设备驱动程序。 例如，如果设备驱动程序不在设备树中，则设备驱动程序的安装可能会出现问题。

有关设备节点调试扩展的详细信息，请参阅 [**！ devnode**](-devnode.md)。

**&lt;-在主机系统上**

1. 若要查看即插即用设备树中的所有设备节点，请输入 **！ devnode 0 1** 命令。 此命令可能需要一到两分钟的时间才能运行。 在此期间，" \* 忙碌" 将显示在 WinDbg 的 "状态" 区域中。

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

2. 使用 Ctrl + F 在生成的输出中搜索以查找设备驱动程序的名称， *sysvad*。

   ![显示搜索字词 sysvad 的 "查找" 对话框](images/sysvad-lab-audio-find-dialog.png)

   名称为的设备节点条目 `sysvad_TabletAudioSample` 将出现在 Syvad 的！ devnode 输出中。

   ```dbgcmd
     DevNode 0xffffe00086e68190 for PDO 0xffffe00089c575a0
       InstancePath is "ROOT\sysvad_TabletAudioSample\0000"
       ServiceName is "sysvad_tabletaudiosample"
       State = DeviceNodeStarted (0x308)
   ...
   ```

   请注意，将显示 PDO 地址和 DevNode 地址。

3. 使用 `!devnode 0 1 sysvad_TabletAudioSample` 命令显示与 Sysvad 设备驱动程序关联的即插即用信息。

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

4. 前一个命令中显示的输出包含与驱动程序的正在运行的实例关联的 PDO，在此示例中为 *0xffffe00089c575a0*。 输入 **！ devobj**<em> &lt; PDO address &gt; </em>命令以显示与 Sysvad 设备驱动程序关联即插即用信息。 使用 **！ devnode** 在你的电脑上显示的 PDO 地址，而不是此处显示的地址。

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

5. **！ Devobj**命令中显示的输出包含附加设备的名称： \\ Driver \\ sysvad \_ tabletaudiosample。 使用带有位掩码2的 **！ drvobj** 命令来显示与连接的设备关联的信息。

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

6. 输入 **！ devstack**<em> &lt; PDO address &gt; </em>命令以显示与设备驱动程序相关即插即用信息。 **！ Devnode 0 1**命令中显示的输出包含与驱动程序的运行实例相关联的 PDO 地址。 在此示例中，它是 *0xffffe00089c575a0*。 使用 **！ devnode** 在你的电脑上显示的 PDO 地址，而不是以下显示的地址。

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

输出显示我们有一个 farily 的简单设备驱动程序堆栈。 Sysvad \_ TabletAudioSample 驱动程序是 PnPManager 节点的子节点。 PnPManager 是根节点。

此图显示了更复杂的设备节点树。

![包含大约20个节点的设备节点树](images/debuglab-image-device-node-tree.png)

**注意**   有关更复杂的驱动程序堆栈的详细信息，请参阅[驱动程序堆栈](../gettingstarted/driver-stacks.md)和[设备节点和设备堆栈](../gettingstarted/device-nodes-and-device-stacks.md)。

 

## <a name="span-idworkingwithbreakpointsspansection-7-working-with-breakpoints"></a><span id="workingwithbreakpoints"></span>第7部分：使用断点


*在第7部分中，你将使用断点来停止特定点处的代码执行。*

**使用命令设置断点**

断点用于在特定代码行处停止执行代码。 然后，可以从该点开始前进，以调试该代码的特定部分。

若要使用调试命令设置断点，请使用下列 **b** 命令之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>bp</p></td>
<td align="left"><p>设置一个断点，该断点将在卸载之前处于活动状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>bu</p></td>
<td align="left"><p>设置在卸载模块时未解析的断点，在模块重新加载时重新启用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bm.exe</p></td>
<td align="left"><p>设置符号的断点。 此命令将适当地使用 bu 或 bp，并允许使用通配符 * 来设置与) 类中的所有方法相同 (的每个符号上的断点。</p></td>
</tr>
</tbody>
</table>

 

1.  使用 WinDbg UI 确认**Debug** &gt; 在当前 WinDbg 会话中启用了 "调试**源" 模式**。

2.  键入以下命令，将本地代码位置添加到源路径。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

3.  键入以下命令，将本地符号位置添加到符号路径中。

    ```dbgcmd
    .sympath+ C:\WDK_Samples\Sysvad
    ```

4.  **设置调试掩码**

    使用驱动程序时，可以方便地查看它可能显示的所有消息。 键入以下项以更改默认调试位掩码，以便从目标系统中的所有调试消息都显示在调试器中。

    ```dbgcmd
    0: kd> ed nt!Kd_DEFAULT_MASK 0xFFFFFFFF
    ```

5.  使用 **bm.exe** 命令设置断点，使用驱动程序名称，后跟函数名称 (AddDevice) 要设置断点的位置，用感叹号分隔。

    ```dbgcmd
    0: kd> bm tabletaudiosample!AddDevice
    breakpoint 1 redefined
      1: fffff801`14b5f000 @!"tabletaudiosample!AddDevice"
    ```

    您可以结合使用不同语法和设置变量，如 &lt; module &gt; ！ &lt;symbol &gt; 、 &lt; class &gt; ：： &lt; 方法 &gt; 、" &lt; file .cpp &gt; ： &lt; 行号 &gt; "，或跳过次数 &lt; 条件 &gt; &lt; \# &gt; 。 有关详细信息，请参阅 [使用断点](using-breakpoints.md)。

6.  列出当前断点以确认是否通过键入 **bl** 命令设置了断点。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`14b5f000     0001 (0001) tabletaudiosample!AddDevice
    ```

7.  在目标系统上重新启动代码执行，方法是键入 "开始" 命令 **g**。

8.  **-&gt;在目标系统上**

    在 Windows 中，通过使用图标或输入 **mmc devmgmt.msc**打开设备管理器。 在 **设备管理器** 展开 " **声音、视频和游戏控制器** " 节点。 选择并按住 (或右键单击) 虚拟音频驱动程序条目，然后从菜单中选择 " **禁用** "。

9.  选择并按住 (或右键单击 "虚拟音频驱动程序" 条目) ，然后从菜单中选择 " **启用** "。
10. **&lt;-在主机系统上**

    这会导致 Windows 重新加载驱动程序，这将调用 AddDevice。 这将导致触发 AddDevice 调试断点，并应终止目标系统上的驱动程序代码的执行。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!AddDevice:
    fffff801`14baf000 4889542410      mov     qword ptr [rsp+10h],rdx
    ```

    如果正确设置了源路径，则应在 AddDevice 例程中停止。

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

11. 通过在代码中键入 **p** 命令或按 F10 来逐行执行代码。 可以从 sysvad AddDevice 代码单步执行到 PpvUtilCall、PnpCallAddDevice，然后转到 PipCallDriverAddDevice Windows 代码。 您可以向 **p** 命令提供一个数字，以单步执行多行（例如 *p 5*）。

12. 完成代码的单步执行后，使用 "转到" 命令 **g** 在目标系统上重新开始执行。

**设置内存访问断点**

还可以设置在访问内存位置时激发的断点。 使用 " **ba** (在 access) 上中断" 命令，使用以下语法。

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
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>e</p></td>
<td align="left"><p>CPU 从地址提取指令时执行 () </p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>读/写 (CPU 读取或写入地址时的) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>w</p></td>
<td align="left"><p>当 CPU 写入地址时写入 () </p></td>
</tr>
</tbody>
</table>

 

请注意，在任何给定时间，只能设置四个数据断点，并由您确保正确对齐数据或不触发断点 (单词必须以2为界限，而 dword 必须可被4整除，并 quadwords 0 或 8) 

例如，若要在特定内存地址上设置读/写断点，请使用如下所示的命令。

```dbgcmd
ba r 4 fffff800`7bc9eff0
```

**修改断点状态**

您可以使用以下命令修改现有断点。

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
<td align="left"><p>连续性</p></td>
<td align="left"><p>从列表中清除断点。 使用 bc * 清除所有断点。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>bd</p></td>
<td align="left"><p>禁用断点。 使用 bd * 禁用所有断点。</p></td>
</tr>
<tr class="even">
<td align="left"><p>必须</p></td>
<td align="left"><p>启用断点。 使用 * 启用所有断点。</p></td>
</tr>
</tbody>
</table>

 

此外，也可以通过选择 "**编辑**断点" 来修改断点 &gt; **breakpoints**。 请注意，"断点" 对话框仅适用于现有的断点。 必须从命令行设置新断点。

**在 MixerVolume 上设置断点**

在加载设备驱动程序之后，将调用音频驱动程序代码的不同部分来响应各种事件。 在下一部分中，我们将设置一个断点，当用户调整虚拟音频驱动程序的音量控件时，将触发该断点。

若要在 MixerVolume 上设置断点，请执行以下步骤。

1.  **&lt;-在主机系统上**

    若要查找更改卷的方法，请使用 x 命令列出包含字符串卷的 CAdapterCommon 中的符号。

    ```dbgcmd
    kd> x tabletaudiosample!CAdapterCommon::*
    ...
    fffff800`7bce26a0 tabletaudiosample!CAdapterCommon::MixerVolumeWrite (unsigned long, unsigned long, long)
    …
    ```

    使用 CTRL + F 在卷的输出中向上搜索，并找到 MixerVolumeWrite 方法。

2.  使用 bc 清除以前的断点 \* 。
3.  使用以下命令在 CAdapterCommon：： MixerVolumeWrite 例程上设置符号断点。

    ```dbgcmd
    kd> bm tabletaudiosample!CAdapterCommon::MixerVolumeWrite
      1: fffff801`177b26a0 @!"tabletaudiosample!CAdapterCommon::MixerVolumeWrite"
    ```

4.  列出断点以确认是否正确设置了断点。

    ```dbgcmd
    kd> bl
    1 e fffff801`177b26a0 [c:\WDK_Samples\audio\sysvad\common.cpp @ 1668]    0001 (0001) tabletaudiosample!CAdapterCommon::MixerVolumeWrite
    ```

5.  在目标系统上重新启动代码执行，方法是键入 "开始" 命令 **g**。

6.  在 "控制面板" 中，选择 "**硬件和声音**" &gt; **Sound**。 选择并按住 (或右键单击) **接收器说明示例** ，然后选择 " **属性**"。 选择 " **级别** " 选项卡。调整滑块音量。

7.  这会导致触发 SetMixerVolume 调试断点，并使目标系统上的驱动程序代码执行停止。

    ```dbgcmd
    kd> g
    Breakpoint 1 hit
    tabletaudiosample!CAdapterCommon::MixerVolumeWrite:
    fffff801`177b26a0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    应在常见 .cpp 中停止此行

    ```dbgcmd
    {
        if (m_pHW)
        {
            m_pHW->SetMixerVolume(Index, Channel, Value);
        }
    } // MixerVolumeWrite
    ```

8.  使用 dv 命令显示当前变量及其值。 本实验室的下一节中提供了有关变量的详细信息。

    ```dbgcmd
    2: kd> dv
               this = 0x00000000`00000010
             ulNode = 0x344
          ulChannel = 0x210a45f8
            lVolume = 0n24
    ```

9.  按 **F10** 单步执行代码。

10. 按 **F5** 完成 MixerVolumeWrite 代码的执行。

**摘要-逐句通过调试器中的代码命令窗口**

以下命令可用于单步执行代码，并使用括号) 中显示的关联键盘短暂切口 (。

-   中断 (Ctrl + Break) -只要系统正在运行且与 WinDbg 通信，则此命令将中断系统 (内核调试器中的序列是 Ctrl + C) 。

-   逐过程执行 (F10) –此命令会导致代码执行一次执行一个语句或一个指令。 如果遇到调用，代码执行将通过调用而不输入被调用的例程。  (如果编程语言为 c 或 c + + 并且 WinDbg 处于源模式，则可以使用**调试** &gt; **源模式**) 打开或关闭源模式。

-    (F11) 中的步骤–此命令类似于 "逐过程"，不同之处在于执行调用会进入被调用例程。

-   跳出 (Shift + F11) –此命令会使执行运行到，并从当前例程退出 (调用堆栈) 中的当前位置。 如果你已看到足够的例程，这会很有用。

-   运行到光标 (F7 或 Ctrl + F10) –将光标置于要执行中断的源或反汇编窗口中，然后按 F7;代码执行将运行到该点。 请注意，如果代码执行流不会到达游标所指示的点 (例如，IF 语句不会执行) ，WinDbg 不会中断，因为代码执行不会到达指示的点。

-   运行 (F5) –运行，直到遇到断点或发生错误检查之类的事件。

**高级选项**

-   将指令设置为当前行 (Ctrl + Shift + I) –在源窗口中，你可以将光标放在一行上，输入此键盘快捷方式，然后，只要你允许使用 F5 或 F10) ，就会立即从该点开始代码执行 (。 如果要重试序列，这会很方便，但需要小心。 例如，寄存器和变量不会设置为，前提是代码执行在自然到达该行。

-   Eip 注册的直接设置-可将值放入 eip 寄存器，并在按 F5 (或 F10、F11 等 ) ，从该地址开始执行。 这类似于将指令设置为游标指定的当前行，只不过指定了程序集指令的地址。

可以更方便地逐句通过 UI，而不是使用命令行，因此建议使用此方法。 如有必要，可在命令行中使用以下命令单步执行源文件：

-   lines-启用源行信息。

-   bp main-在模块的开头设置初始断点。

-   l + t-步进将由源行完成。

-   选择 "**调试** &gt; **源" 模式**进入源模式; `L+t` 命令不够。

-   "+ s" 将在提示符处显示源行。

-   g-运行程序，直到进入 "main"。

-   p-执行一个源行。

有关详细信息，请参阅调试参考文档 [中的 WinDbg 中的源代码调试](source-window.md) 。

**在代码中设置断点**

可以通过添加 `DebugBreak()` 语句并重新生成项目，然后重新安装驱动程序来在代码中设置断点。 此断点将在每次启用驱动程序时激发，因此它将是在早期开发阶段（而不是在生产代码中）使用的一种技术。 此方法并不像使用断点命令动态设置断点那样灵活。

提示：你可能想要将 Sysvad 驱动程序的副本与添加的断点一起用于进一步实验室工作。

1.  通过将 `DebugBreak()` 语句添加到示例代码中，设置每次运行 AddDevice 方法时出现的中断。

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

2.  按照前面介绍的所有步骤在 Microsoft Visual Studio 中重建驱动程序，然后将其重新安装到目标计算机。 安装更新的驱动程序之前，请务必卸载现有的驱动程序。
3.  清除任何以前的断点，并确保将调试器附加到目标 PC。

4.  当代码运行并到达语句时 `DebugBreak` ，将停止执行，并显示一条消息。

    ```dbgcmd
    KERNELBASE!DebugBreak:
    77b3b770 defe     __debugbreak
    ```

## <a name="span-idlookingatvariablesspanspan-idlookingatvariablesspanspan-idlookingatvariablesspansection-8-display-variables"></a><span id="LookingAtVariables"></span><span id="lookingatvariables"></span><span id="LOOKINGATVARIABLES"></span>第8部分：显示变量


*在第8节中，您将使用调试器命令来显示变量。*

在代码执行时检查变量以确认代码按预期方式工作可能非常有用。 此实验室检查变量，因为音频驱动程序产生声音。

1.  使用 **dv** 命令检查与 tabletaudiosample 关联的区域设置变量！CMiniportWaveRT：： New \* 。

    ```dbgcmd
    kd> dv tabletaudiosample!CMiniportWaveRT::New*
    ```

2.  清除前面的断点

    ```dbgcmd
    bc *
    ```

3.  使用以下命令在 CMiniportWaveCyclicStreamMSVAD 例程上设置符号断点。

    ```dbgcmd
    0: kd> bm tabletaudiosample!CMiniportWaveRT::NewStream
      1: fffff801`177dffc0 @!"tabletaudiosample!CMiniportWaveRT::NewStream"
    ```

4.  在目标系统上重新启动代码执行，方法是键入 "开始" 命令 **g**。

5.  **-&gt; 在目标系统上**

    查找小的媒体文件 (例如带有 .wav 文件扩展名的 Windows 通知声音文件) 并选择要播放的文件。 例如，可以使用位于 Windows Media 目录中的 Ring05。 \\

6.  **&lt;-在主机系统上**

    播放媒体文件时，应触发断点，并应停止目标系统上的驱动程序代码的执行。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::NewStream:
    fffff801`177dffc0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

    源代码窗口应在 Newstream.ischecked 函数的入口上突出显示大括号。

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

7.  **局部变量**

    您可以通过键入 **dv** 命令显示给定帧的所有局部变量的名称和值。

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

8.  **使用 DML 显示变量**

    若要使用 DML 浏览变量，请选择带下划线的元素。 "选择" 操作将生成一个 [**dx (显示 NatVis 表达式) **](dx--display-visualizer-variables-.md) 命令，可用于向下钻取嵌套的数据结构。

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

    您可以通过键入来找到全局变量的内存位置 **。 &lt;变量名称 &gt; **。

    ```dbgcmd
    0: kd> ? signalProcessingMode
    Evaluate expression: -52768896396472 = ffffd001`c8acd348
    ```

10. 这会返回变量的内存位置，在本例中为 *ffffd001 \` c8acd348*。 通过使用上一命令返回的内存位置转储键入 **dd** 命令的位置值，可以查看内存位置的内容。

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

11. 还可以将变量名称与 **dd** 命令一起使用。

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

    使用 "**查看** &gt; **局部变量**" 菜单项可显示局部变量。 此接口还提供了向下钻取更复杂的数据结构的功能。

    ![显示示例代码局部变量和命令窗口的 windbg](images/sysvad-lab-display-variables.png)

13. 在突出显示 ntStatus = IsFormatSupported (Pin、捕获、DataFormat) 的情况下，使用 p 或 F10 前进到代码中的10行：代码行。

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

14. 使用 **dv** 命令显示给定帧的所有局部变量的名称和值。 请注意，所需的值与上一次运行此命令时的值不同，因为已运行更改本地变量的其他代码，但某些变量现在不在当前框架中，或者其值已更改。

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

## <a name="span-idviewingcallstacksspansection-9-view-call-stacks"></a><span id="viewingcallstacks"></span>第9节：查看调用堆栈


*在第9节中，你将查看调用堆栈以检查调用方/ (代码。*

调用堆栈是已导致程序计数器当前位置的函数调用的链。 调用堆栈上的 top 函数是当前函数，下一个函数是调用当前函数的函数，依此类推。

若要显示调用堆栈，请使用 k \* 命令：

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
<td align="left"><p>显示参数的堆栈和完整列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>kn</p></td>
<td align="left"><p>允许你查看堆栈，其中包含框架信息。</p></td>
</tr>
</tbody>
</table>

 

如果要保留可用的调用堆栈，可选择 "**查看** &gt; **调用堆栈**" 以查看。 选择窗口顶部的列以切换其他信息的显示。

!["windbg 调用堆栈" 窗口](images/sysvad-lab-call-stack.png)

此输出在调试处于中断状态的示例适配器代码时显示调用堆栈。

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

可以使用 DML 进一步浏览代码。 选择第一个00条目时， [**. frame (设置本地上下文) **](-frame--set-local-context-.md) 命令用于设置上下文，然后， [**Dv (显示本地变量) **](dv--display-local-variables-.md) 命令显示局部变量。

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

## <a name="span-iddisplayingprocessesandthreadsspansection-10-display-processes-and-threads"></a><span id="displayingprocessesandthreads"></span>第10部分：显示进程和线程


*在第10节中，您将使用调试器命令来显示进程和线程。*

**Process**

若要更改当前进程上下文，请使用. process &lt; process &gt; 命令。 下面的示例演示如何识别进程并向其切换上下文。

-   使用 `!process` 命令显示播放声音所涉及的当前进程。

    有关详细信息，请参阅[ **！进程**](-process.md)

输出显示该进程与 audiodg.exe 相关联。 如果仍处于本主题上一部分所述的断点，则当前进程应与 audiodg.exe 映像关联。

**&lt;-在主机系统上**

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

请注意，与此进程关联的一个线程处于 "正在运行" 状态。 此线程支持在命中断点时播放媒体剪辑。

使用 **！ process 0 0** 命令显示所有进程的摘要信息。 在命令输出中，使用 CTRL + F 查找与 audiodg.exe 映像关联的进程的进程 ID。 在下面所示的示例中，进程 ID 为 *ffffe001d147c840*。

记录与计算机上 audiodg.exe 相关联的进程 ID，以便稍后在本实验室中使用。 \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

```dbgcmd
...

PROCESS ffffe001d147c840
    SessionId: 0  Cid: 10f0    Peb: ee6cf8a000  ParentCid: 0434
    DirBase: d2122000  ObjectTable: ffffc0001f191ac0  HandleCount: <Data Not Accessible>
    Image: audiodg.exe
...
```

将 g 输入到调试器中，以便向前运行代码，直到媒体剪辑完成播放。 然后，通过按 Ctrl + ScrLk (Ctrl + Break) 来中断调试器，使用！ process 命令确认现在正在运行不同的进程。

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

以上输出显示， *ffffe001cd0ad040* 的其他系统进程正在运行。 映像名称显示系统，而不是 audiodg.exe。

现在使用！ process 命令切换到与 audiodg.exe 关联的进程。 在此示例中，进程 ID 为 *ffffe001d147c840*。 将示例中的进程 ID 替换为之前记录的进程 ID。

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

由于此代码不处于活动状态，因此所有线程都处于 "等待" 状态。

**线程**

用于查看和设置线程的命令与进程的命令非常相似。 使用 [**！ thread**](-thread.md) 命令查看线程。 使用 [**. thread**](-thread--set-register-context-.md) 设置当前线程。

若要浏览与 media player 关联的线程，请再次播放媒体剪辑。 如果在上一节中描述的断点仍存在，则将在 audiodg.exe 的上下文中停止。

使用！ thread-1 0 显示当前线程的简短信息。 这会显示线程地址、线程和进程 Id、线程环境块 (TEB) 地址、Win32 函数的地址 (（如果创建了要运行的线程的任何) ）以及线程的计划状态。

```dbgcmd
0: kd> !thread -1 0
THREAD ffffe001d3a27040  Cid 10f0.17f4  Teb: 000000ee6cf9d000 Win32Thread: 0000000000000000 RUNNING on processor 0
```

若要查看有关正在运行的线程的详细信息，请键入 [**！ thread**](-thread.md)。 应显示类似于以下内容的信息。

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

使用 k 命令查看与线程关联的调用堆栈。

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

将 g 输入到调试器中，以便向前运行代码，直到媒体剪辑完成播放。 然后，通过按下 Ctrl-ScrLk (Ctrl-Break) 来中断调试器，使用！ thread 命令确认现在正在运行不同的线程。

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

映像名称为 rundll32.exe，这实际上并不是与播放媒体剪辑关联的图像名称。

**注意**   若要设置当前线程，请键入 thread &lt; thread number &gt; 。

有关线程和进程的详细信息，请参阅以下参考资料：

[线程和进程](threads-and-processes.md)

[更改上下文](changing-contexts.md)

 

## <a name="span-idirqlregistersmemoryspansection-11-irql-registers-and-disassembly"></a><span id="irqlregistersmemory"></span>第11节： IRQL、寄存器和反汇编


### <a name="span-idview_the_saved_irqlspanview-the-saved-irql"></a><span id="view_the_saved_irql"></span>查看保存的 IRQL

*在第11节中，您将显示 regsisters 的 IRQL 和内容。*

**&lt;-在主机系统上**

中断请求级别 (IRQL) 用于管理中断服务的优先级。 每个处理器都有一个可以提高或降低线程的 IRQL 设置。 在处理器的 IRQL 设置下或之下发生的中断会被屏蔽，并且不会影响当前操作。 超出处理器的 IRQL 设置的中断优先于当前操作。 在调试程序发生中断之前，在目标计算机的当前处理器上，此 [**！ irql**](-irql.md) 扩展显示中断请求级别 (irql) 。 当目标计算机中断到调试器时，IRQL 会发生更改，但在调试器中断之前有效的 IRQL 会被保存，并由！ IRQL 显示。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanview-the-registers-and-disassembly"></a><<span id="viewingtheregisters"></span>查看寄存器和反汇编

**查看寄存器**

使用 [**r (寄存器) **](r--registers-.md) 命令在当前处理器上显示当前线程的注册内容。

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

或者，您可以通过选择 "**查看**寄存器" 来显示寄存器内容 &gt; **Registers**。

![显示大约12个寄存器的 "windbg 寄存器" 窗口](images/sysvad-lab-audio-display-registers.png)

在单步执行汇编语言代码执行和其他情况时，查看寄存器的内容会很有帮助。 有关详细信息，请参阅 [**r (寄存器) **](r--registers-.md)。

有关寄存器内容的信息，请参阅 [X86 体系结构](x86-architecture.md) 和 [x64 体系结构](x64-architecture.md)。

**反汇编**

您可以通过选择 "**查看**反汇编" 来反汇编正在执行的代码，以查看正在运行的程序集语言代码 &gt; **Disassembly**。

![windbg 反汇编窗口](images/sysvad-lab-audio-disassembly-window.png)

有关汇编语言反汇编的详细信息，请参阅 [带批注的 X86 反汇编](annotated-x86-disassembly.md) 和 [带批注的 x64 反汇编](annotated-x64-disassembly.md)。

## <a name="span-idworkingwithmemoryspansection-12-work-with-memory"></a><span id="workingwithmemory"></span>第12部分：使用内存


*在第12节中，您将使用调试器命令来显示内存的内容。*

**查看内存**

您可能需要检查内存以确定问题或检查变量、指针等等。 可以通过键入以下**d \* &lt; &gt; 地址**命令之一来显示内存。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>db</p></td>
<td align="left"><p>在字节值和 ASCII 字符中显示数据。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dd</p></td>
<td align="left"><p>将数据显示为双宽字 (4 个字节) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>du</p></td>
<td align="left"><p>将数据显示为 Unicode 字符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>dw</p></td>
<td align="left"><p>将数据显示为字值 (2 个字节) 和 ASCII 字符。</p></td>
</tr>
</tbody>
</table>

 

**注意**   如果尝试显示无效地址，则其内容将显示为问号 (？ ) 。

 

或者，您可以通过选择 "**查看**内存" 来查看内存 &gt; **Memory**。 使用 **显示格式** 向下下拉以更改显示内存的方式。

![windbg "查看内存" 窗口](images/sysvad-lab-audio-memory-display.png)

1.  若要查看与卷控件关联的数据，请使用 bm.exe 命令将断点设置为在 PropertyHandlerAudioEngineVolumeLevel 例程上激发。 设置新断点之前，我们将使用 bc 清除前面的所有断点 \* 。

    ```dbgcmd
    kd> bc *
    ```

2.  使用 bm.exe 命令设置要在 PropertyHandlerAudioEngineVolumeLevel 例程上触发的断点。

    ```dbgcmd
    kd> bm tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

3.  列出断点以确认是否正确设置了断点。

    ```dbgcmd
    kd> bl
      1: fffff80f`02c3a4b0 @!"tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume"
    ```

4.  使用 **g** 命令重新启动代码执行。

    在目标系统上，调整系统托盘中的卷。 这将导致引发断点。

    ```dbgcmd
    Breakpoint 1 hit
    tabletaudiosample!CMiniportWaveRT::SetDeviceChannelVolume:
    fffff80f`02c3a4b0 44894c2420      mov     dword ptr [rsp+20h],r9d
    ```

5.  使用 "**查看** &gt; **本地**" 菜单项可显示局部变量。 记下 IVolume 变量的当前值。

6.  通过键入 **dt** 命令和变量的名称，可以在示例代码中显示 IVolume 变量的数据类型和当前值。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xa011ea50 Type long
    0n-6291456
    ```

7.  输入 SetDeviceChannelVolume 时命中断点。

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

8.  尝试使用 [**dt (显示类型) **](dt--display-type-.md) 命令在内存位置显示值。

    ```dbgcmd
    kd> dt dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n0
    ```

    由于仍要定义变量，因此不包含信息。

9.  按 F10 前进到 SetDeviceChannelVolume 中代码的最后一行。

    ```dbgcmd
        return ntStatus;
    ```

10. 使用 [**dt (显示类型) **](dt--display-type-.md) 命令，在内存位置显示值。

    ```dbgcmd
    kd> dt lVolume
    Local var @ 0xffffb780b7eee664 Type long
    0n-6291456
    ```

    变量处于活动状态，此时将在此示例中显示值6291456。

11. 还可以通过使用 [**？ (计算 Expression) **](---evaluate-expression-.md) 命令来显示 IVolume 的内存位置。

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

12. 显示的地址 *ffffb780 \` B7eee664* 是 lVolume 变量的地址。 使用 dd 命令显示该位置的内存内容。

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

13. 通过指定范围参数 L4，可以显示地址的前四个字节。

    ```dbgcmd
    kd> dd ffffb780`b7eee664 l4
    ffffb780`b7eee664  ffa00000 00000018 00000000 c52d7008
    ```

14. 若要查看显示的不同类型的内存输出，请键入 **du**、 **da** 和 **db** 命令。

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

    使用 df float 选项可将数据显示为单精度浮点数， (4 个字节) 。

    ```dbgcmd
    df ffffb780`b7eee664 
    ffffb780`b7eee664          -1.#QNAN   3.3631163e-044                0        -2775.002
    ffffb780`b7eee674          -1.#QNAN  -5.8032637e+019         -1.#QNAN        -2775.002
    ffffb780`b7eee684          -1.#QNAN                0         -1.#QNAN                0
    ffffb780`b7eee694          -1.#QNAN         -1.#QNAN         -1.#QNAN  -2.8479408e-005
    ```

**写入内存**

与用于读取内存的命令类似，你可以使用 e \* 命令更改内存内容。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Command</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ea</p></td>
<td align="left"><p>不以 NULL 结尾的 ASCII 字符串 () </p></td>
</tr>
<tr class="even">
<td align="left"><p>eu</p></td>
<td align="left"><p>Unicode 字符串 (不以 NULL 结尾</p></td>
</tr>
<tr class="odd">
<td align="left"><p>new</p></td>
<td align="left"><p>字值 (2 个字节) </p></td>
</tr>
<tr class="even">
<td align="left"><p>eza</p></td>
<td align="left"><p>以 NULL 结尾的 ASCII 字符串</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ezu</p></td>
<td align="left"><p>以 NULL 结尾的 Unicode 字符串</p></td>
</tr>
<tr class="even">
<td align="left"><p>eb</p></td>
<td align="left"><p>字节值</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ed</p></td>
<td align="left"><p>双字值 (4 个字节) </p></td>
</tr>
</tbody>
</table>

 

下面的示例演示如何覆盖内存。

1.  首先，找到示例代码中使用的 lVolume 的地址。

    ```dbgcmd
    kd> ? lVolume
    Evaluate expression: -79711507126684 = ffffb780`b7eee664
    ```

2.  使用 **eb** 命令覆盖包含新字符的内存地址。

    ```dbgcmd
    kd> eb 0xffffb780`b7eee664 11 11 11 11 11
    ```

3.  显示内存位置，以确认已通过键入 **db** 命令覆盖了这些字符。

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

或者，你可以在 "监视" 或 "局部变量" 窗口中修改内存的内容。 对于 "监视" 窗口，可能会看到超出当前帧上下文的变量。 如果修改它们不在上下文中，则不相关。

## <a name="span-idendingthesessionspansection-13-end-the-windbg-session"></a><span id="endingthesession"></span>第13部分：结束 WinDbg 会话


**&lt;-在主机系统上**

若要结束用户模式调试会话，请将调试器返回到休眠模式，然后将目标应用程序设置为再次运行，请输入 **qd** (Quit 并分离) 命令。

请确保并使用 **g** 命令让目标计算机运行代码，使其可以使用。 使用 * * bc * * * 清除任何断点也是一个不错的主意 \\ ，这样，目标计算机将不会中断，而会尝试连接到主机计算机调试器。

```dbgcmd
0: kd> qd
```

有关详细信息，请参阅调试参考文档 [中的在 WinDbg 结束调试会话](ending-a-debugging-session-in-windbg.md) 。

## <a name="span-idwindowsdebuggingresourcesspansection-14-windows-debugging-resources"></a><span id="windowsdebuggingresources"></span>第14节： Windows 调试资源


有关其他信息，请访问 Windows 调试。 请注意，其中的一些书籍将使用旧版 Windows （如 Windows Vista）的示例，但讨论的概念适用于大多数 Windows 版本。

**书籍**

-   Mario Hewardt 和 Daniel Pravat 的*高级 Windows 调试*

-   *在 Windows 调试中：通过 Tarik Soulami 在 windows®中调试和跟踪策略的实用指南*

-   *Windows 内部机制* ，Russinovich，David 为所罗门群岛和 Alex Ionescu

**视频**

碎片整理工具显示 WinDbg 剧集13-29 <https://channel9.msdn.com/Shows/Defrag-Tools>

**培训供应商：**

OSR <https://www.osr.com/>


## <a name="see-also"></a>另请参阅

[Windows 调试入门](getting-started-with-windows-debugging.md) 