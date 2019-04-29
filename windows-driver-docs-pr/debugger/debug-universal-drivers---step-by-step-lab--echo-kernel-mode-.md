---
title: 调试通用驱动程序的分步实验室 （Echo 内核模式）
description: 此实验室中引入了 WinDbg 内核调试程序。 使用 WinDbg 调试 echo 内核模式示例驱动程序代码。
ms.assetid: 3FBC3693-4288-42BA-B1E8-84DC2A9AFFD9
keywords:
- 调试实验室
- step-by-step
- ECHO
ms.date: 03/28/2019
ms.localizationpriority: medium
ms.openlocfilehash: 8900b9f6098ccf2c560d21b4cf941c484ff089c3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357167"
---
# <a name="span-iddebuggerdebuguniversaldrivers-stepbysteplabechokernel-modespandebug-universal-drivers---step-by-step-lab-echo-kernel-mode"></a><span id="debugger.debug_universal_drivers_-_step_by_step_lab__echo_kernel-mode_"></span>调试通用驱动程序的执行步骤的实验室 （Echo 内核模式）


此实验室中引入了 WinDbg 内核调试程序。 使用 WinDbg 调试 echo 内核模式示例驱动程序代码。

## <a name="span-idlabobjectivesspanspan-idlabobjectivesspanspan-idlabobjectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>实验室目的


此实验室包括相关的练习，引入的调试工具、 介绍常见的调试命令、 中断点的用法和显示了如何使用调试扩展。

在此实验中，实时内核调试连接用于采用以下机制：

-   使用 Windows 调试器命令
-   使用标准命令 （调用堆栈、 变量、 线程、 IRQL）
-   使用高级驱动程序调试命令 (！ 命令)
-   使用符号
-   设置断点的实时调试
-   查看调用堆栈
-   显示插设备树
-   使用线程和进程的上下文

**请注意**时使用的 Windows 调试器，有两种类型的调试可执行的用户或内核模式调试。

*用户模式下*-应用程序和子系统在用户模式下在计算机上运行。 在用户模式下运行的进程执行此操作在其自己的虚拟地址空间内。 它们被限制直接访问系统，包括系统硬件，其使用，并可能危及系统完整性的系统的其他部分为未分配的内存的很多部分。 在用户模式下运行的进程是从系统和其他用户模式进程有效地隔离的因为它们不能干扰这些资源。

*内核模式*-内核模式是在其中运行的系统和特权程序运行的处理器访问模式。 内核模式代码有权访问的系统，任何部分，并且不受限制用户模式代码等。 它可以访问在用户模式或内核模式中运行的任何其他进程的任何部分。 在内核模式下运行的核心操作系统功能和许多硬件设备驱动程序。

此实验室将重点介绍内核模式调试，因为这是用来调试多个设备驱动程序的方法。


本练习中介绍了在用户模式和内核模式调试期间经常使用的调试命令。 本练习还介绍了调试扩展 (有时称为"！ 命令")，用于内核模式调试。

## <a name="span-idlabsetupspanspan-idlabsetupspanspan-idlabsetupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>实验室设置


你将需要以下硬件以便能够完成实验室。

-   便携式计算机或台式计算机 （主机） 运行 Windows 10
-   便携式计算机或台式计算机 （目标） 运行 Windows 10
-   网络中心/路由器和网络电缆连接两台 Pc
-   访问 internet 以下载符号文件

你将需要以下软件才能将无法完成该实验。

-   Visual Studio 2017
-   适用于 Windows 10 的 Windows 软件开发工具包 (SDK)
-   适用于 Windows 10 的 Windows 驱动程序工具包 (WDK)
-   适用于 Windows 10 示例 echo 驱动程序

实验室有以下 11 个部分。

-   [第 1 部分：连接到内核模式 WinDbg 会话](#connectto)
-   [第 2 部分：内核模式调试命令和技术](#kernelmodedebuggingcommandsandtechniques)
-   [第 3 部分：下载并构建 KMDF 通用 Echo 驱动程序](#download)
-   [第 4 部分：在目标系统上安装回送 KMDF 驱动程序示例](#install)
-   [第 5 部分：使用 WinDbg 显示有关驱动程序的信息](#usewindbgtodisplayinformation)
-   [第 6 部分：显示插设备树信息](#displayingtheplugandplaydevicetree)
-   [第 7 部分：使用断点和源代码](#workingwithbreakpoints)
-   [第 8 部分：查看变量和调用堆栈](#viewingvariables)
-   [第 9 部分：显示进程和线程](#displayingprocessesandthreads)
-   [第 10 部分：IRQL，寄存器并结束 WinDbg 会话](#irqlregistersmemory)
-   [第 11 节：Windows 调试资源](#windowsdebuggingresources)

## <a name="span-idconnecttospanspan-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span><span id="CONNECTTO"></span>第 1 部分：连接到内核模式 WinDbg 会话


*在第 1 部分，将配置网络在主机和目标系统上进行调试。*

此实验室中的 Pc 需要将配置为使用以太网网络连接进行内核调试。

此实验使用两台 Pc。 在运行 Windows 的调试程序*主机*上运行的系统和 KMDF Echo 驱动程序*目标*系统。

 使用网络中心/路由器和网络电缆连接两台 Pc。

![与双向箭头连接的两台 pc](images/debuglab-image-targethostdrawing1.png)

若要使用的内核模式应用程序和使用 WinDbg，我们建议通过以太网传输使用 KDNET。 有关如何使用以太网传输协议的信息，请参阅[开始使用 WinDbg （内核模式）](getting-started-with-windbg--kernel-mode-.md)。 有关设置目标计算机的详细信息，请参阅[手动驱动程序部署准备一台计算机](https://msdn.microsoft.com/windows-drivers/develop/preparing_a_computer_for_manual_driver_deployment)并[设置向上 KDNET 网络内核调试自动](setting-up-a-network-debugging-connection-automatically.md)。

### <a name="span-idconfigurekernelmodedebuggingusingethernetspanspan-idconfigurekernelmodedebuggingusingethernetspanspan-idconfigurekernelmodedebuggingusingethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="Configure__kernel_mode_debugging_using_ethernet"></span><span id="configure__kernel_mode_debugging_using_ethernet"></span><span id="CONFIGURE__KERNEL_MODE_DEBUGGING_USING_ETHERNET"></span>配置内核模式 – 调试使用以太网

若要启用内核模式下在目标系统上进行调试，请执行以下步骤。

**&lt;在主机系统**

1. 打开命令提示符上的主机系统和类型**ipconfig**以确定其 IP 地址。

```console
C:\>ipconfig
Windows IP Configuration
Ethernet adapter Ethernet:
   Connection-specific DNS Suffix  . :
   Link-local IPv6 Address . . . . . : fe80::c8b6:db13:d1e8:b13b%3
   Autoconfiguration IPv4 Address. . : 169.182.1.1
   Subnet Mask . . . . . . . . . . . : 255.255.0.0
   Default Gateway . . . . . . . . . :
```

2. 记录主机系统的 IP 地址： \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**-&gt; 在目标系统上**

3. 打开在目标系统上的命令提示符，并使用**ping**命令来确认这两个系统之间的网络连接。 而不是示例输出所示的 169.182.1.1 使用主机系统所记录的实际 IP 地址。

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

启用内核模式下通过完成以下步骤在目标系统上进行调试。

> [!IMPORTANT]
> 使用 BCDEdit 以更改启动信息之前可能需要暂时挂起如 BitLocker 和安全引导测试 PC 上的 Windows 安全功能。
> 测试完成后重新启用这些安全功能和安全功能将被禁用时适当地管理测试 PC。

1. 在目标计算机上，以管理员身份打开命令提示符窗口。 输入此命令以启用调试。

    ```console
    C:\> bcdedit /set {default} DEBUG YES
    ```

2. 键入以下命令以启用测试签名。

    ```console
    C:\> bcdedit /set TESTSIGNING ON 
    ```


3. 键入以下命令以设置主机系统的 IP 地址。 使用你之前记录未显示的一个主机系统的 IP 地址。

    ```console
    C:\> bcdedit /dbgsettings net hostip:192.168.1.1 port:50000 key:1.2.3.4
    ```

**警告**若要增加连接的安全性和降低风险随机客户端调试器连接请求，请考虑使用自动生成的随机密钥。 有关详细信息，请参阅[设置向上 KDNET 网络内核调试自动](setting-up-a-network-debugging-connection-automatically.md)。

4. 键入以下命令以确认 dbgsettings 它们设置正确。

    ```console
    C:\> bcdedit /dbgsettings
    key                     1.2.3.4
    debugtype               NET
    hostip                  169.168.1.1
    port                    50000
    dhcp                    Yes
    The operation completed successfully.
    ```

**注意**  
**防火墙和调试器**

如果从防火墙，看到一个弹出消息，并且你想要使用调试器，检查**所有这三个**的框。

![windows 安全警报的 windows 防火墙已阻止此应用的某些功能 ](images/debuglab-image-firewall-dialog-box.png)



**&lt;在主机系统**

1. 在主计算机上，以管理员身份打开命令提示符窗口。 我们将使用 x64 版本的 WinDbg.exe 已作为 Windows 工具包安装的一部分安装 Windows Driver Kit (WDK) 中。 默认情况下它位于此处。

    ```console
    C:\> Cd C:\Program Files(x86)\Windows Kits\10\Debuggers\x64 
    ```

> [!NOTE]
> 此实验室假定这两台 Pc 上的目标和主机运行 Windows 的 64 位版本。 如果这不是这样，最好的方法是运行在目标主机上运行工具的同一"位数"。 例如，如果目标是正在运行 32 位 Windows，在主机上运行 32 版本的调试器。 有关详细信息，请参阅[选择 32 位或 64 位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
> 

2. 使用远程用户调试使用以下命令启动 WinDbg。 我们前面设置的密钥和端口的值匹配在目标系统上使用 BCDEdit。

    ```console
    WinDbg –k net:port=50000,key=1.2.3.4
    ```

**-&gt;在目标系统上**

重新启动目标系统。

**&lt;在主机系统**

在一分钟或两个，应在主机系统上显示调试输出。

```dbgcmd
Microsoft (R) Windows Debugger Version 10.0.17074.1002 AMD64
Copyright (c) Microsoft Corporation. All rights reserved.

Using NET for debugging
Opened WinSock 2.0
Waiting to reconnect...
Connected to target 169.182.1.1 on port 50005 on local IP 169.182.1.2
You can get the target MAC address by running .kdtargetmac command.
Connected to Windows 10 16299 x64 target at (Wed Feb 28 17:16:23.051 2018 (UTC - 8:00)), ptr64 TRUE
Kernel Debugger connection established.  (Initial Breakpoint requested)
Symbol search path is: srv*
Executable search path is: 
Windows 10 Kernel Version 16299 MP (4 procs) Free x64
Product: WinNt, suite: TerminalServer SingleUserTS
Built by: 16299.15.amd64fre.rs3_release.170928-1534
Machine Name:
Kernel base = 0xfffff800`9540d000 PsLoadedModuleList = 0xfffff800`95774110
Debug session time: Wed Feb 28 17:16:23.816 2018 (UTC - 8:00)
System Uptime: 0 days 0:00:20.534
```

调试器命令窗口是在 WinDbg 中主要的调试信息窗口。 您可以输入的调试器命令，在此窗口中查看命令输出。

调试器命令窗口拆分为两个窗格。 在窗口底部的小窗格 （命令项窗格） 中键入命令，并在更大窗口的顶部窗格中查看命令输出。

在命令项窗格中，使用向上箭头和向下箭头键可以滚动浏览命令历史记录。 命令出现时，你可以对其进行编辑，或按**ENTER**运行命令。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="KernelModeDebuggingCommandsAndTechniques"></span><span id="kernelmodedebuggingcommandsandtechniques"></span><span id="KERNELMODEDEBUGGINGCOMMANDSANDTECHNIQUES"></span>第 2 部分：内核模式调试命令和技术


*在第 2 部分，您将使用调试命令来显示有关目标系统的信息。*

**&lt;在主机系统**

**让调试器标记语言 (DML) 使用.prefer\_dml**

一些调试命令的显示文本使用调试器标记语言，可以单击快速收集的详细信息。

1. 在 WinDBg 中使用 Ctrl + Break (Scroll Lock) 分解为目标系统上运行的代码。 可能需要一些时间才能在目标系统进行响应。

![windows 调试器实时内核连接进行连接时显示命令窗口输出](images/debuglab-image-winddbg-hh.png)


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

6. 你可以验证你正在使用正确的内核模式进程通过显示已加载的模块，通过键入[ **lm （列表加载模块）** ](lm--list-loaded-modules-.md) WinDbg 窗口命令。

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

**请注意**已省略的输出指示"... "在此实验中。



7. 若要请求有关的特定模块的详细的信息，请使用 v （详细） 选项所示。

```dbgcmd
0: Kd> lm v m tcpip
Browse full module list
start             end                 module name
fffff801`09eeb000 fffff801`0a157000   tcpip      (no symbols)           
    Loaded symbol image file: tcpip.sys
    Image path: \SystemRoot\System32\drivers\tcpip.sys
    Image name: tcpip.sys
    Browse all global symbols  functions  data
    Timestamp:        Sun Nov 09 18:59:03 2014 (546029F7)
    CheckSum:         00263DB1
    ImageSize:        0026C000
    Translations:     0000.04b0 0000.04e4 0409.04b0 0409.04e4

Unable to enumerate user-mode unloaded modules, Win32 error 0n30
```

8. 因为我们尚未设置符号路径和已加载的符号，有限的信息可在调试器中。

## <a name="span-iddownloadspanspan-iddownloadspanspan-iddownloadspansection-3-download-and-build-the-kmdf-universal-echo-driver"></a><span id="Download"></span><span id="download"></span><span id="DOWNLOAD"></span>第 3 部分：下载并构建 KMDF 通用 echo 驱动程序

*在第 3 部分，将下载并构建 KMDF 通用 echo 驱动程序。*

通常情况下，您应该使用与你自己的驱动程序代码使用 WinDbg 时。 若要熟悉 WinDbg 操作，请使用 KMDF 模板"的 Echo"示例驱动程序。 提供源代码，它还将更轻松地了解在 WinDbg 中显示的信息。 此外，此示例用于说明如何可以单一单步执行本机内核模式代码。 这种技术都是用于调试复杂的内核模式代码问题非常有用。

若要下载并生成 Echo 示例音频驱动程序时，执行以下步骤。

1.  **下载并从 GitHub 提取 KMDF Echo 示例**

    浏览器可用于在此处查看 GitHub 中的 echo 示例：

    [https://github.com/Microsoft/Windows-driver-samples/tree/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    你可以阅读此处的示例：

    <https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md>

    您可以浏览所有通用驱动程序示例：

    <https://github.com/Microsoft/Windows-driver-samples>

    KMDF Echo 示例位于常规文件夹中。

    ![github windows 的驱动程序的示例突出显示的常规文件夹和下载 zip 按钮](images/debuglab-image-github.png)

    a. 此实验中，演示如何下载一个 zip 文件中的通用驱动程序示例。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b. Master.zip 文件下载到本地硬盘。

    c. 右键单击*Windows 驱动程序示例 master.zip*，然后选择**全部提取**。 指定新文件夹，或浏览到一个现有将存储提取的文件。 例如，可以指定*c:\\DriverSamples\\* 作为文件提取到其中的新文件夹。

    d. 提取文件后，导航到以下子文件夹。

    *C:\\DriverSamples\\general\\echo\\kmdf*

2.  **在 Visual Studio 中打开驱动程序解决方案**

    在 Microsoft Visual Studio 中，单击**文件** &gt; **打开** &gt; **项目/解决方案...** 并导航到包含所提取的文件的文件夹 (例如， *c:\\DriverSamples\\常规\\echo\\kmdf*)。 双击*kmdfecho*解决方案文件以将其打开。

    在 Visual Studio 中，找到解决方案资源管理器。 (如果尚未打开，请将此选择**解决方案资源管理器**从**视图**菜单。)在解决方案资源管理器，可以看到一个包含三个项目的解决方案。

    ![visual studio 中的使用 device.c 文件加载从 kmdfecho 项目](images/debuglab-image-echo-visual-studio.png)

3.  **设置示例的配置和平台**

    在解决方案资源管理器中右键单击**kmdfecho （3 个项目） 的解决方案**，然后选择**Configuration Manager**。 请确保配置和平台设置是相同的三个项目。 默认情况下的配置设置为"Win10 Debug"，并将所有项目的平台设置为"Win64"。 如果你进行任何配置和/或平台更改为一个项目，必须进行的剩余三个项目相同的更改。

4.  **设置运行时库**

    设置运行时库-打开 echo 驱动程序的属性页，并找到**C /C++**  &gt; **代码生成**。  将运行时库 DLL 版本更改为非 DLL 版本。 如果没有此设置，您必须单独安装到目标计算机的 MSVC 运行时。

    ![突出显示此运行时库设置回显属性页](images/debuglab-image-echoapp-properties.png)

5.  **检查驱动程序签名**

    此外，驱动程序的属性上请确保**驱动程序签名** &gt; **登录模式**设置为"测试登录"。 这是必需的因为 Windows 需要的驱动程序签名。

    ![突出显示的登录模式设置回送属性页](images/debuglab-image-echoapp-driver-signing.png)

6.  **使用 Visual Studio 生成示例**

    在 Visual Studio 中，单击**构建** &gt; **生成解决方案**。

    如果一切顺利，生成 windows 应显示一条指示对于所有三个项目生成成功消息。

7.  **找到的内置驱动程序文件**

    在文件资源管理器，导航到包含示例提取的文件的文件夹。 例如，你可以导航到*c:\\DriverSamples\\常规\\echo\\kmdf*，如果这是你在前面指定的文件夹。 在该文件夹中，已编译的驱动程序文件的位置而异的配置和平台设置中选择**Configuration Manager**。 例如，如果保留默认设置保持不变，然后将已编译的驱动程序文件将保存到名为的文件夹 *\\x64\\调试*适用于 64 位，调试版本。

    导航到包含自动同步驱动程序的生成的文件的文件夹：

    *C:\\DriverSamples\\常规\\echo\\kmdf\\驱动程序\\AutoSync\\x64\\调试*。 

    该文件夹应包含这些文件：

    | 文件     | 描述                                                                       |
    |----------|-----------------------------------------------------------------------------------|
    | Echo.sys | 驱动程序文件中。                                                                  |
    | Echo.inf | 一个包含安装驱动程序所需信息的信息 (INF) 文件。 |

    此外，echoapp.exe 文件生成，并且它应该位于此处：*C:\\DriverSamples\\general\\echo\\kmdf\\exe\\x64\\Debug*

    | 文件        | 描述                                                                       |
    |-------------|-----------------------------------------------------------------------------------|
    | EchoApp.exe | 一个与 echo.sys 驱动程序进行通信的命令提示符可执行的测试文件。 |     

8.  找到 USB 拇指驱动器或网络共享设置为将内置的驱动程序文件和测试 EchoApp 复制从主机到目标系统。

在下一步部分中，会将代码复制到目标系统中，并安装和测试驱动程序。

## <a name="span-idinstallspanspan-idinstallspanspan-idinstallspansection-4-install-the-kmdf-echo-driver-sample-on-the-target-system"></a><span id="Install"></span><span id="install"></span><span id="INSTALL"></span>第 4 部分：在目标系统上安装 KMDF echo 驱动程序示例

*在第 4 部分，您将使用 devcon 安装 echo 示例驱动程序。*

**-&gt; 在目标系统上**

安装该驱动程序的计算机称为*目标计算机*或*测试计算机*。 通常情况下，这是在其开发和生成的驱动程序包的计算机不同的计算机。 开发和生成该驱动程序的计算机称为*主机计算机*。

将驱动程序包移动到目标计算机和安装该驱动程序的过程称为*部署*驱动程序。 你可以自动或手动部署示例 echo 驱动程序。

手动部署驱动程序之前，必须通过启用测试签名来准备目标计算机。 此外需要在 WDK 安装中找到 DevCon 工具。 之后，您就可以运行内置驱动程序示例。

若要在目标系统上安装该驱动程序，请执行以下步骤。

**启用测试签名驱动程序**

启用的功能，若要运行测试签名驱动程序：

a. 打开 Windows 设置。

b. 在更新和安全中，选择**恢复**。

c. 在下，高级启动时，单击**立即重新启动**。

d. 当 PC 重新启动时，选择**启动选项**。 在 Windows 10 中，选择**进行故障排除** > **高级选项** > **启动设置**，然后单击重新启动按钮。 

e. 通过按选择禁用强制驱动程序签名**F7**密钥。

f. 重新启动目标计算机。


**&lt;在主机系统**

导航到 WDK 安装中的工具文件夹并找到 DevCon 工具。 例如，在以下文件夹中查看：

*C:\\Program Files (x86)\\Windows 工具包\\10.0\\工具\\x64\\devcon.exe*内置的驱动程序包的目标上创建一个文件夹 (例如， *C:\\EchoDriver*)。 从主计算机上的前面所述的内置驱动程序复制的所有文件并将其保存到目标计算机创建的文件夹。

在主机系统上找到.cer 证书，而是在包含内置的驱动程序文件的文件夹中的主机计算机上的同一文件夹中。 在目标计算机上，右键单击该证书文件，然后单击**安装**，然后按照提示安装测试证书。

如果设置的目标计算机需要更多详细的说明，请参阅[手动驱动程序部署准备计算机](../develop/preparing-a-computer-for-manual-driver-deployment.md)。

**-&gt; 在目标系统上**

**安装驱动程序**

以下说明介绍如何安装和测试的示例驱动程序。 以下是将用于安装驱动程序的 devcon 工具的常规语法：

*devcon install &lt;INF file&gt; &lt;hardware ID&gt;*

安装此驱动程序所需的 INF 文件*echo.inf*。 Inf 文件包含用于安装的硬件 ID *echo.sys*。 Echo 示例硬件 ID 是**根\\ECHO**。

在目标计算机上，以管理员身份打开命令提示符窗口。 导航到驱动程序的包文件夹，并输入以下命令：

**devcon 安装 echo.inf 根\\ECHO**如果你收到一条错误消息*devcon*未被识别，请尝试添加的路径*devcon*工具。 例如，如果复制到名为的文件夹*c:\\工具*，然后尝试使用以下命令：

**c:\\工具\\devcon 安装 echo.inf 根\\ECHO** ，该值指示测试驱动程序未签名的驱动程序将出现一个对话框。 单击**仍然安装此驱动程序**以继续。

![windows 安全警告-windows 无法验证该驱动程序软件的发布者](images/debuglab-image-install-security-warning.png)

有关详细说明，请参阅[配置一台计算机的驱动程序部署、 测试和调试](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/provision-a-target-computer-wdk-8-1)。

已成功安装后的示例驱动程序，现在，你准备好对其进行测试。

**检查驱动程序在设备管理器**

在目标计算机，在命令提示符窗口中，输入**devmgmt**打开设备管理器。 在设备管理器中，在视图菜单上选择按类型列出的设备。 在设备树中，找到*示例 WDF Echo 驱动程序*示例设备节点中。

![设备管理器树中突出显示的示例 wdf echo 驱动程序](images/debuglab-image-device-manager-echo.png)

**测试驱动程序**

类型**echoapp**以启动测试回显应用程序，以确认该驱动程序可正常运行。

```dbgcmd
C:\Samples\KMDF_Echo_Sample> echoapp
DevicePath: \\?\root#sample#0005#{cdc35b6e-0be4-4936-bf5f-5537380a7c1a}
Opened device successfully
512 Pattern Bytes Written successfully
512 Pattern Bytes Read successfully
Pattern Verified successfully
30720 Pattern Bytes Written successfully
30720 Pattern Bytes Read successfully
Pattern Verified successfully
```

## <a name="span-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="UseWinDbgToDisplayInformation"></span><span id="usewindbgtodisplayinformation"></span><span id="USEWINDBGTODISPLAYINFORMATION"></span>第 5 部分：使用 WinDbg 显示有关驱动程序的信息

*第 5 节中将设置符号路径，并使用内核调试器命令以显示有关 KMDF echo 示例驱动程序信息。*

通过执行以下步骤来查看有关该驱动程序的信息。

**&lt;在主机系统**

1.  如果关闭调试器时，打开管理员命令提示符窗口中再次使用以下命令。

    ```dbgcmd
    WinDbg -k net:port=50000,key=1.2.3.4
    ```

2.  使用 Ctrl + Break (Scroll Lock) 分解为目标系统上运行的代码。

**设置符号路径**

1.  若要向 Microsoft 符号服务器在 WinDbg 环境中设置符号路径，请使用 **.symfix**命令。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  若要添加你的本地符号位置使用本地符号，添加以下路径 using **.sympath +** ，然后 **.reload /f**。

    ```dbgcmd
    0: kd> .sympath+ C:\DriverSamples\general\echo\kmdf
    0: kd> .reload /f
    ```

    **请注意** **.reload**命令 **/f** force 选项将删除指定的模块的所有符号信息，然后重新加载符号。 在某些情况下，此命令还将重新加载或卸载该模块本身。



**请注意**必须加载正确的符号使用 WinDbg 提供的高级的功能。 如果不具有正确配置的符号，将收到消息，指示的符号不可用时尝试使用依赖于符号的功能。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```



**注意**  
**符号服务器**

有多种方法可用于使用符号。 在许多情况下，您可以从符号服务器，Microsoft 提供了在需要时访问符号配置 PC。 本演练假设将使用此方法。 如果你的环境中的符号不在不同的位置，来修改使用该位置的步骤。 有关其他信息，请参阅[符号存储区和符号服务器](symbol-stores-and-symbol-servers.md)。



**注意**  
**了解源代码符号要求**

若要执行源代码调试，必须生成选中 （调试） 版本的二进制文件的位置。 编译器会创建符号文件 （.pdb 文件）。 这些符号文件将显示在调试器的二进制说明如何与源行相对应。 此外必须可以访问调试器本身的实际源文件。

符号文件不包含源代码的文本。 对于调试，最好是如果链接器不会优化你的代码。 源调试和本地变量的访问权限是更困难，并且有时几乎不可能，如果代码已经过优化。 如果您无法查看本地变量或源行，设置以下生成选项：

```console
set COMPILE_DEBUG=1
set ENABLE_OPTIMIZER=0
```



1. 键入以下命令在命令区域中的调试器显示 echo 驱动程序有关的信息：

   ```dbgcmd
   0: kd> lm m echo* v
   Browse full module list
   start             end                 module name
   fffff801`4ae80000 fffff801`4ae89000   ECHO       (private pdb symbols)  C:\Samples\KMDF_ECHO_SAMPLE\echo.pdb
       Loaded symbol image file: ECHO.sys
       Image path: \SystemRoot\system32\DRIVERS\ECHO.sys
       Image name: ECHO.sys
   ...  
   ```

   有关信息，请参阅[ **lm**](lm--list-loaded-modules-.md)。

2. 因为我们设置首选\_dml = 1 更早版本，输出的某些元素是可单击的快速链接。 单击*浏览所有全局符号链接*中调试输出以显示有关以字母开头的项符号信息"a"。

   ```dbgcmd
   0: kd> x /D Echo!a*
   ```

3. 事实证明，echo 示例不包含任何符号以字母开头的"a"，因此若要显示的 echo 驱动程序与关联的符号以回显，开头的所有信息键入 * * x ECHO ！Echo\\* * *。

   ```dbgcmd
   0: kd> x ECHO!Echo*
   fffff801`0bf95690 ECHO!EchoEvtIoQueueContextDestroy (void *)
   fffff801`0bf95000 ECHO!EchoEvtDeviceSelfManagedIoStart (struct WDFDEVICE__ *)
   fffff801`0bf95ac0 ECHO!EchoEvtTimerFunc (struct WDFTIMER__ *)
   fffff801`0bf9b120 ECHO!EchoEvtDeviceSelfManagedIoSuspend (struct WDFDEVICE__ *)
   ...
   ```

   有关信息，请参阅[ **（检查符号） x**](x--examine-symbols-.md)。

4. **！ Lmi**扩展显示有关模块的详细的信息。 类型 **！ lmi echo**。 输出应类似于如下所示的文本。

   ```dbgcmd
   0: kd> !lmi echo
   Loaded Module Info: [echo] 
            Module: ECHO
      Base Address: fffff8010bf94000
        Image Name: ECHO.sys
   … 
   ```

5. 使用 **！ dh**扩展名，即可显示标头信息，如下所示。

   ```dbgcmd
   0: kd> !dh echo

   File Type: EXECUTABLE IMAGE
   FILE HEADER VALUES
        14C machine (i386)
          6 number of sections
   54AD8A42 time date stamp Wed Jan 07 11:34:26 2015
   ...
   ```

6. **设置调试掩码**

   以下内容，以更改默认调试位掩码，以便所有调试从目标系统的消息将显示在调试器中的类型。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0xFFFFFFFF
   ```

   某些驱动程序将使用掩码为 0xFFFFFFFF 时显示的其他信息。 如果你想要减少显示的信息，请将掩码设置为 0x00000000。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0x00000000
   ```

   使用 dd 命令以显示确认掩码设置为显示所有调试器消息。 

   ```dbgcmd
   0: kd> dd nt!kd_DEFAULT_MASK 
   fffff802`bb4057c0  ffffffff 00000000 00000000 00000000
   fffff802`bb4057d0  00000000 00000000 00000000 00000000
   fffff802`bb4057e0  00000001 00000000 00000000 00000000
   fffff802`bb4057f0  00000000 00000000 00000000 00000000
   fffff802`bb405800  00000000 00000000 00000000 00000000
   fffff802`bb405810  00000000 00000000 00000000 00000000
   fffff802`bb405820  00000000 00000000 00000000 00000000
   fffff802`bb405830  00000000 00000000 00000000 00000000
   ```


## <a name="span-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="DisplayingThePlugAndPlayDeviceTree"></span><span id="displayingtheplugandplaydevicetree"></span><span id="DISPLAYINGTHEPLUGANDPLAYDEVICETREE"></span>第 6 部分：显示插设备树信息

*在第 6 节，将显示有关 echo 示例设备驱动程序的信息和何处插设备树中。*

Plug and Play 设备树中的设备驱动程序有关的信息可用于故障排除。 例如，如果设备驱动程序不是驻留在设备树中，可以安装设备驱动程序出现问题。

有关设备节点调试扩展的详细信息，请参阅[ **！ devnode**](-devnode.md)。

**&lt;在主机系统**

1. 若要查看在插设备树中的所有设备节点，请输入 **！ devnode 0 1**命令。

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
   …
   ```

2. 使用 Ctrl + F 来生成，以查找设备驱动程序，该名称在输出中搜索*echo*。

   ![查找对话框显示要搜索的术语回显](images/debuglab-image-find-dialog.png)

3. 应加载 echo 设备驱动程序。 使用 **！ devnode 0 1 echo**命令以显示插信息与我们回显设备驱动程序相关联，如下所示。

   ```dbgcmd
   0: Kd> !devnode 0 1 echo
   Dumping IopRootDeviceNode (= 0xffffe0007b725d30)
   DevNode 0xffffe0007b71a630 for PDO 0xffffe0007b71a960
     InstancePath is "ROOT\SAMPLE\0000"
     ServiceName is "ECHO"
     State = DeviceNodeStarted (0x308)
     Previous State = DeviceNodeEnumerateCompletion (0x30d)
   …
   ```

4. 前一个命令中显示的输出包括与正在运行的驱动程序实例相关联的是 PDO，在此示例中它是*0xffffe0007b71a960*。 输入 **！ devobj**<em>&lt;PDO 地址&gt;</em>命令以显示与 echo 设备驱动程序相关联的插信息。 使用 PDO 解决 **！ devnode**显示在您 PC 上，不是如下所示。

   ```dbgcmd
   0: kd> !devobj 0xffffe0007b71a960
   Device object (ffffe0007b71a960) is for:
    0000000e \Driver\PnpManager DriverObject ffffe0007b727e60
   Current Irp 00000000 RefCount 0 Type 00000004 Flags 00001040
   Dacl ffffc102c9b36031 DevExt 00000000 DevObjExt ffffe0007b71aab0 DevNode ffffe0007b71a630 
   ExtensionFlags (0x00000800)  DOE_DEFAULT_SD_PRESENT
   Characteristics (0x00000180)  FILE_AUTOGENERATED_DEVICE_NAME, FILE_DEVICE_SECURE_OPEN
   AttachedDevice (Upper) ffffe000801fee20 \Driver\ECHO
   Device queue is not busy.
   ```

5. 中显示的输出 **！ 0 1 devnode**命令包含与正在运行的驱动程序实例关联的 PDO 地址，在此示例很*0xffffe0007b71a960*。 输入 **！ devstack**<em>&lt;PDO 地址&gt;</em>命令以显示与设备驱动程序相关联的插信息。 使用 PDO 解决 **！ devnode**显示在您 PC 上，不是如下所示。

   ```dbgcmd
   0: kd> !devstack 0xffffe0007b71a960
     !DevObj           !DrvObj            !DevExt           ObjectName
     ffffe000801fee20  \Driver\ECHO       ffffe0007f72eff0  
   > ffffe0007b71a960  \Driver\PnpManager 00000000  0000000e
   !DevNode ffffe0007b71a630 :
     DeviceInst is "ROOT\SAMPLE\0000"
     ServiceName is "ECHO"
   ```

输出显示有相当简单的设备驱动程序堆栈。 Echo 驱动程序是 PnPManager 节点的子节点。 PnPManager 是根节点。

\Driver\ECHO      

\Driver\PnpManager

下图显示了更复杂的设备节点树。

![设备有大约具有 20 个节点的节点树](images/debuglab-image-device-node-tree.png)

**请注意**有关更复杂的驱动程序堆栈的详细信息，请参阅[驱动程序堆栈](https://msdn.microsoft.com/library/windows/hardware/hh439632)并[设备节点和设备堆栈](https://msdn.microsoft.com/library/windows/hardware/ff554721)。



## <a name="span-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspansection-7-working-with-breakpoints-and-source-code"></a><span id="WorkingWithBreakpoints"></span><span id="workingwithbreakpoints"></span><span id="WORKINGWITHBREAKPOINTS"></span>第 7 部分：使用断点和源代码

*第 7 节中将设置断点并单步执行完内核模式下的源代码。*

**注意**  
**使用命令设置断点**

若要能够单步执行代码，并检查在真实时间中的变量的值，我们需要启用断点，并将路径设置为的源代码。

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





有关详细信息，请参阅[源代码调试在 WinDbg 中](source-window.md)调试的参考文档中。

**&lt;在主机系统**

1.  使用 WinDbg UI 以确认**调试** &gt; **源模式**当前 WinDbg 会话中启用。

2.  通过键入以下命令将你的本地代码位置添加到源路径。

    ```dbgcmd
    .srcpath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

3.  通过键入以下命令将你的本地符号位置添加到符号路径。

    ```dbgcmd
    .sympath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

4.  我们将使用**x**命令来检查 echo 驱动程序，以确定要使用断点的函数名称与相关联的符号。 我们可以使用通配符或 Ctrl + F 来定位**DeviceAdd**函数名称。

    ```dbgcmd
    0: kd> x ECHO!EchoEvt*
    8b4c7490          ECHO!EchoEvtIoQueueContextDestroy (void *)
    8b4c7000          ECHO!EchoEvtDeviceSelfManagedIoStart (struct WDFDEVICE__ *)
    8b4c7820          ECHO!EchoEvtTimerFunc (struct WDFTIMER__ *)
    8b4cb0e0          ECHO!EchoEvtDeviceSelfManagedIoSuspend (struct WDFDEVICE__ *)
    8b4c75d0          ECHO!EchoEvtIoWrite (struct WDFQUEUE__ *, struct WDFREQUEST__ *, unsigned int)
    8b4cb170          ECHO!EchoEvtDeviceAdd (struct WDFDRIVER__ *, struct 
    …
    ```

    上面的输出显示**DeviceAdd**我们回显驱动程序的方法是*ECHO ！EchoEvtDeviceAdd*。

    或者，我们可以查看源代码，以找到的断点的所需的函数名称。

5.  设置的断点**bm**命令使用驱动程序后, 跟函数名称的名称 (例如**AddDevice**) 在你想要设置断点，分隔一个感叹号。 我们将使用**AddDevice**观看所加载的驱动程序。

    ```dbgcmd
    0: kd> bm ECHO!EchoEvtDeviceAdd
      1: fffff801`0bf9b1c0 @!"ECHO!EchoEvtDeviceAdd"
    ```

    **注意**  
    可以使用不同的语法与设置变量，如结合&lt;模块&gt;！&lt;符号&gt;，&lt;类&gt;::&lt;方法&gt;，&lt;file.cpp&gt;:&lt;行号&gt;，或跳过数乘以&lt;条件&gt; &lt; \# &gt;。 有关详细信息，请参阅[WinDbg 和其他 Windows 调试器中的条件断点](setting-a-conditional-breakpoint.md)。



6.  列出要确认通过键入来设置了断点的当前断点**bl**命令。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`0bf9b1c0     0001 (0001) ECHO!EchoEvtDeviceAdd
    ```

    在上面所示的输出中的"e"指示启用断点数 1 激发。

7.  重新在目标系统上的执行代码启动通过键入**转**命令**g**。

8.  **-&gt; 在目标系统上**

    在 Windows 中，打开**设备管理器**使用的图标，或通过输入**mmc devmgmt.msc**。 在设备管理器中，展开**示例**节点。

9.  右键单击 KMDF Echo 驱动程序条目，然后选择**禁用**菜单中。

10. 再次右键单击 KMDF Echo 驱动程序条目，然后选择**启用**菜单中。

11. **&lt;在主机系统**

    启用驱动程序后， [ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)调试断点应触发，并且在目标系统上的驱动程序代码的执行应暂停。 当到达断点时，应开始时停止执行*AddDevice*例程。 调试命令输出会显示"命中断点 1"。

    ![windbg 显示示例代码局部变量和命令窗口](images/debuglab-image-breakpoint-echo-deviceadd.png)

12. 通过键入逐步执行代码--逐行**p**命令或按 F10，直到达到以下结尾[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程。 大括号字符"}"将突出显示所示。

    ![显示在开头 adddevice 例程时突出显示的大括号字符的代码窗口](images/debuglab-image-breakpoint-end-deviceadd.png)

13. 在下一部分中，我们将执行 DeviceAdd 代码后检查变量的状态。

**注意**  
**修改断点的状态**

可以使用以下命令来修改现有断点：

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



或者，您还可以通过单击修改断点**编辑** &gt; **断点**在 WinDbg 中。 请注意，断点对话框仅适用于现有断点。 必须从命令行设置新断点。



**注意**  
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
<th align="left">Option</th>
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



请注意，在任何给定时间只能设置四个数据断点，它将由您来确保将正确对齐数据或将不会触发该断点 （字必须以整除的地址结尾的一半，dword 值必须是整除 4和四字的 0 或 8)。

例如，若要设置特定的内存地址的读/写断点，可以使用如下命令。

```dbgcmd
ba r 4 0x0003f7bf0
```



**注意**  
**从调试器命令窗口中逐句通过代码**

以下是可以使用的命令来逐句通过代码 （具有关联的键盘快捷方式显示在括号中）。

-   中断 (Ctrl + Break)-此命令将中断一个系统，只要系统正在运行，并且是与 WinDbg （内核调试程序中的序列是 Ctrl + C） 的通信中。

-   运行到光标处 （F7 或 Ctrl + F10） – 将光标放在源代码或反汇编窗口中要执行中断操作，然后按 F7;执行代码将运行到该点。 请注意，是否代码执行流将不会访问点表示游标 （IF 语句不会执行），WinDbg 将不会中断，因为代码执行未到达指定的点。

-   运行 (F5) – 运行直到遇到断点时或发生的 bug 检查之类的事件发生。

-   步跃 (f10) – 此命令将导致代码执行来继续执行一个语句或一次一条指令。 如果遇到调用，代码执行将通过调用而无需输入调用的例程。 (如果编程语言为 C 或C++和 WinDbg 位于源模式中，源模式可以打开或关闭使用**调试**&gt;**源模式**)。

-   步骤中 (F11)-此命令是逐过程类似，只不过调用的执行将进入被调用例程。

-   跳出 (Shift + F11) – 此命令将导致执行运行并从当前退出例程 （调用堆栈中的当前位置）。 这是很有用，如果您已了解足够多的例程。



有关详细信息，请参阅[源代码调试在 WinDbg 中](source-window.md)调试的参考文档中。

## <a name="span-idviewingvariablesspanspan-idviewingvariablesspanspan-idviewingvariablesspansection-8-viewing-variables-and-call-stacks"></a><span id="ViewingVariables"></span><span id="viewingvariables"></span><span id="VIEWINGVARIABLES"></span>第 8 部分：查看变量和调用堆栈

*在第 8 节，将显示有关变量的信息，并调用堆栈。*

此实验室假定在你已停止[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程使用前面所述的过程。 若要查看输出显示于此，请重复前面所述的步骤，如有必要。

**&lt;在主机系统**

**显示变量**

使用**视图**&gt; **本地**菜单项以显示本地变量。

![windbg 局部变量窗口](images/debuglab-image-display-variables.png)

**全局变量**

也可以键入找到的全局变量地址位置 *？&lt;变量名&gt;*。

**本地变量**

可以通过键入显示的名称和值的给定的框架的所有局部变量**dv**命令。

```dbgcmd
0: kd> dv
         Driver = 0x00001fff`7ff9c838
     DeviceInit = 0xffffd001`51978190
         status = 0n0
```

**调用堆栈**

**注意**  
调用堆栈是导致程序计数器当前位置的函数调用链。 在调用堆栈顶部的函数是当前函数，而下一步函数调用当前函数的函数，等等。

若要显示调用堆栈，请使用 k\*命令。

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





**&lt;在主机系统**

1. 如果你想要保留可用的调用堆栈，则可以单击**视图** &gt; **调用堆栈**查看它。 单击可切换的附加信息显示在窗口顶部的列。

![windbg 显示调用堆栈窗口](images/debuglab-image-display-callstacks.png)

2. 使用**kn**命令，以调试示例适配器代码中中断状态时显示调用堆栈。

```dbgcmd
3: kd> kn
# Child-SP          RetAddr           Call Site
00 ffffd001`51978110 fffff801`0942f55b ECHO!EchoEvtDeviceAdd+0x66 [c:\Samples\kmdf echo sample\c++\driver\autosync\driver.c @ 138]
01 (Inline Function) --------`-------- Wdf01000!FxDriverDeviceAdd::Invoke+0x30 [d:\wbrtm\minkernel\wdf\framework\shared\inc\private\common\fxdrivercallbacks.hpp @ 61]
02 ffffd001`51978150 fffff801`eed8097d Wdf01000!FxDriver::AddDevice+0xab [d:\wbrtm\minkernel\wdf\framework\shared\core\km\fxdriverkm.cpp @ 72]
03 ffffd001`51978570 fffff801`ef129423 nt!PpvUtilCallAddDevice+0x35 [d:\9142\minkernel\ntos\io\pnpmgr\verifier.c @ 104]
04 ffffd001`519785b0 fffff801`ef0c4112 nt!PnpCallAddDevice+0x63 [d:\9142\minkernel\ntos\io\pnpmgr\enum.c @ 7397]
05 ffffd001`51978630 fffff801`ef0c344f nt!PipCallDriverAddDevice+0x6e2 [d:\9142\minkernel\ntos\io\pnpmgr\enum.c @ 3390]
...
```

调用堆栈显示了内核 (nt) 到插代码 （即插即用），名为的 code 驱动程序框架 (WDF)，随后调用 echo 驱动程序**DeviceAdd**函数。

## <a name="span-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspansection-9-displaying-processes-and-threads"></a><span id="DisplayingProcessesAndThreads"></span><span id="displayingprocessesandthreads"></span><span id="DISPLAYINGPROCESSESANDTHREADS"></span>第 9 部分：显示进程和线程

### <a name="span-idprocessesspanspan-idprocessesspanspan-idprocessesspanprocesses"></a><span id="Processes"></span><span id="processes"></span><span id="PROCESSES"></span>Processes

*在第 9 节，将显示有关进程和线程在内核模式下运行的信息。*

**注意**  
可以显示或通过设置进程信息[ **！ 过程**](-process.md)调试器扩展。 我们将设置断点，以检查时，将会播放声音，将使用的过程。



1. **&lt;在主机系统**

   类型**dv**命令，检查与关联的区域设置变量**EchoEvtIo**例程所示。

   ```dbgcmd
   0: kd> dv ECHO!EchoEvtIo*
   ECHO!EchoEvtIoQueueContextDestroy
   ECHO!EchoEvtIoWrite
   ECHO!EchoEvtIoRead         
   ```

2. 清除上一个断点使用 * * bc \\* * *。

   ```dbgcmd
   0: kd> bc *  
   ```

3. 3. 设置符号断点**EchoEvtIo**例程使用以下命令。

   ```dbgcmd
   0: kd> bm ECHO!EchoEvtIo*
     2: aade5490          @!”ECHO!EchoEvtIoQueueContextDestroy”
     3: aade55d0          @!”ECHO!EchoEvtIoWrite”
     4: aade54c0          @!”ECHO!EchoEvtIoRead”
   ```

4. 列出要确认正确设置了断点的断点。

   ```dbgcmd
   0: kd> bl
   1 e aabf0490 [c:\Samples\kmdf echo sample\c++\driver\autosync\queue.c @ 197]    0001 (0001) ECHO!EchoEvtIoQueueContextDestroy
   ...
   ```

5. 类型**g**重新启动代码执行。

   ```dbgcmd
   0: kd> g
   ```

6. **-&gt; 在目标系统上**

   在目标系统上运行 EchoApp.exe 驱动程序测试程序。

7. **&lt;在主机系统**

   测试应用运行时，将调用该驱动程序中的 I/O 例程。 这会导致断点激发，并在目标系统上的驱动程序代码的执行都将停止。

   ```dbgcmd
   Breakpoint 2 hit
   ECHO!EchoEvtIoWrite:
   fffff801`0bf95810 4c89442418      mov     qword ptr [rsp+18h],r8
   ```

8. 使用 **！ 过程**命令以显示当前所涉及的进程中运行 echoapp.exe。

   ```dbgcmd
   0: kd> !process
   PROCESS ffffe0007e6a7780
       SessionId: 1  Cid: 03c4    Peb: 7ff7cfec4000  ParentCid: 0f34
       DirBase: 1efd1b000  ObjectTable: ffffc001d77978c0  HandleCount:  34.
       Image: echoapp.exe
       VadRoot ffffe000802c79f0 Vads 30 Clone 0 Private 135. Modified 5. Locked 0.
       DeviceMap ffffc001d83c6e80
       Token                             ffffc001cf270050
       ElapsedTime                       00:00:00.052
       UserTime                          00:00:00.000
       KernelTime                        00:00:00.000
       QuotaPoolUsage[PagedPool]         33824
       QuotaPoolUsage[NonPagedPool]      4464
       Working Set Sizes (now,min,max)  (682, 50, 345) (2728KB, 200KB, 1380KB)
       PeakWorkingSetSize                652
       VirtualSize                       16 Mb
       PeakVirtualSize                   16 Mb
       PageFaultCount                    688
       MemoryPriority                    BACKGROUND
       BasePriority                      8
       CommitCharge                      138

           THREAD ffffe00080e32080  Cid 03c4.0ec0  Teb: 00007ff7cfece000 Win32Thread: 0000000000000000 RUNNING on processor 1
   ```

   该输出显示过程都与 echoapp.exe 命中的断点上驱动程序写入事件时正在运行的关联。 有关详细信息，请参阅[ **！ 过程**](-process.md)。

9. 使用 **！ process 0 0**以显示所有进程的摘要信息。 在输出中，使用 CTRL + F 来查找与 echoapp.exe 映像关联的进程的相同过程地址。 在如下所示示例中，进程地址是 ffffe0007e6a7780。

   ```dbgcmd
   ...

   PROCESS ffffe0007e6a7780
       SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
       DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
       Image: echoapp.exe

   ...
   ```

10. 与 echoapp.exe 以更高版本在此实验室中使用关联的记录进程 ID。 CTRL + C，还可用于将地址复制到复制缓冲区以供将来使用。

    \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_（echoapp.exe 进程地址）

11. 输入**g**调试器要前滚 echoapp.exe 完成运行之前运行此代码中所需的方式。 它将在读取命中了断点，并编写大量的时间的事件。 Echoapp.exe 完成后，在中中断到调试器，通过按 CTRL + ScrLk (Ctrl + Break)。

12. 使用 **！ 过程**命令以确认现在运行不同的进程。 在输出如下所示，映像值为进程*系统*不同于*Echo*图像值。

    ```dbgcmd
    1: kd> !process
    PROCESS ffffe0007b65d900
        SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
        DirBase: 001ab000  ObjectTable: ffffc001c9a03000  HandleCount: 786.
        Image: System
        VadRoot ffffe0007ce45930 Vads 14 Clone 0 Private 22. Modified 131605. Locked 64.
        DeviceMap ffffc001c9a0c220
        Token                             ffffc001c9a05530
        ElapsedTime                       21:31:02.516
    ...
    ```

    上面的输出显示系统进程 ffffe0007b65d900 正在运行，当我们停止 OS。

13. 现在，使用 **！ 过程**命令以尝试查看已与 echoapp.exe 之前记录相关联的进程 ID。 提供你的 echoapp.exe 进程地址之前，而不是如下所示的示例过程地址记录。

    ```dbgcmd
    0: kd> !process ffffe0007e6a7780
    TYPE mismatch for process object at 82a9acc0
    ```

    进程对象不再可用，作为 echoapp.exe 进程是不再运行。

### <a name="span-idthreadsspanspan-idthreadsspanspan-idthreadsspanthreads"></a><span id="Threads"></span><span id="threads"></span><span id="THREADS"></span>线程

**注意**  
若要查看和设置线程的命令是非常类似于那些进程。 使用[ **！ 线程**](-thread.md)命令查看线程。 使用[ **.thread** ](-thread--set-register-context-.md)设置当前线程。



1.  **&lt;在主机系统**

    输入**g**进入重新启动目标系统上的执行代码的调试器。

2.  **-&gt; 在目标系统上**

    在目标系统上运行 EchoApp.exe 驱动程序测试程序。

3.  **&lt;在主机系统**

    将命中断点并且执行代码将暂停。

    ```dbgcmd
    Breakpoint 4 hit
    ECHO!EchoEvtIoRead:
    aade54c0 55              push    ebp
    ```

4.  若要查看正在运行的线程，请键入[ **！ 线程**](-thread.md)。 应显示类似于以下信息：

    ```dbgcmd
    0: kd>  !thread
    THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
    IRP List:
        ffffe0007bc5be10: (0006,01f0) Flags: 00060a30  Mdl: 00000000
    Not impersonating
    DeviceMap                 ffffc001d83c6e80
    Owning Process            ffffe0008096c900       Image:         echoapp.exe
    ...
    ```

    记下的映像名称*echoapp.exe*，指示我们正在查看的测试应用程序与关联的线程。

5.  4. 使用 **！ 过程**命令，以确定这是否与 echoapp.exe 关联的进程中运行的唯一线程。 请注意，在过程中正在运行的线程的线程数是运行在同一线程 ！ thread 命令显示。

    ```dbgcmd
    0: kd> !process
    PROCESS ffffe0008096c900
        SessionId: 1  Cid: 0b28    Peb: 7ff7d00df000  ParentCid: 0f34
        DirBase: 1fb746000  ObjectTable: ffffc001db6b52c0  HandleCount:  34.
        Image: echoapp.exe
        VadRoot ffffe000800cf920 Vads 30 Clone 0 Private 135. Modified 8. Locked 0.
        DeviceMap ffffc001d83c6e80
        Token                             ffffc001cf5dc050
        ElapsedTime                       00:00:00.048
        UserTime                          00:00:00.000
        KernelTime                        00:00:00.000
        QuotaPoolUsage[PagedPool]         33824
        QuotaPoolUsage[NonPagedPool]      4464
        Working Set Sizes (now,min,max)  (681, 50, 345) (2724KB, 200KB, 1380KB)
        PeakWorkingSetSize                651
        VirtualSize                       16 Mb
        PeakVirtualSize                   16 Mb
        PageFaultCount                    686
        MemoryPriority                    BACKGROUND
        BasePriority                      8
        CommitCharge                      138

            THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
    ```

6.  使用 **！ process 0 0 命令**找到两个进程地址相关的进程并记录这些过程解决此处。

    Cmd.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    ```dbgcmd
    0: kd> !process 0 0 

    …

    PROCESS ffffe0007bbde900
        SessionId: 1  Cid: 0f34    Peb: 7ff72dfa7000  ParentCid: 0c64
        DirBase: 19c5fa000  ObjectTable: ffffc001d8c2f300  HandleCount:  31.
        Image: cmd.exe
    …
    PROCESS ffffe0008096c900
        SessionId: 1  Cid: 0b28    Peb: 7ff7d00df000  ParentCid: 0f34
        DirBase: 1fb746000  ObjectTable: ffffc001db6b52c0  HandleCount:  34.
        Image: echoapp.exe
    …
    ```

    **请注意**也可以使用 **！ 处理 0 17**以显示有关每个进程的详细的信息。 此命令的输出可能很长。 可以使用 Ctrl + F 搜索输出。



7.  使用 **！ 过程**命令列出运行您的 PC 这两个进程的进程信息。 提供从进程地址你 **！ process 0 0**输出，不是地址如下所示。

    此示例输出是前面记录的 cmd.exe 进程 ID。 请注意，此进程 ID 的映像名称 cmd.exe。

    ```dbgcmd
    0: kd>  !process ffffe0007bbde900
    PROCESS ffffe0007bbde900
        SessionId: 1  Cid: 0f34    Peb: 7ff72dfa7000  ParentCid: 0c64
        DirBase: 19c5fa000  ObjectTable: ffffc001d8c2f300  HandleCount:  31.
        Image: cmd.exe
        VadRoot ffffe0007bb8e7b0 Vads 25 Clone 0 Private 117. Modified 20. Locked 0.
        DeviceMap ffffc001d83c6e80
        Token                             ffffc001d8c48050
        ElapsedTime                       21:33:05.840
        UserTime                          00:00:00.000
        KernelTime                        00:00:00.000
        QuotaPoolUsage[PagedPool]         24656
        QuotaPoolUsage[NonPagedPool]      3184
        Working Set Sizes (now,min,max)  (261, 50, 345) (1044KB, 200KB, 1380KB)
        PeakWorkingSetSize                616
        VirtualSize                       2097164 Mb
        PeakVirtualSize                   2097165 Mb
        PageFaultCount                    823
        MemoryPriority                    FOREGROUND
        BasePriority                      8
        CommitCharge                      381

            THREAD ffffe0007cf34880  Cid 0f34.0f1c  Teb: 00007ff72dfae000 Win32Thread: 0000000000000000 WAIT: (UserRequest) UserMode Non-Alertable
                ffffe0008096c900  ProcessObject
            Not impersonating
    ...
    ```

    此示例输出是前面记录的 echoapp.exe 进程 ID。

    ```dbgcmd
    0: kd>  !process ffffe0008096c900
    PROCESS ffffe0008096c900
        SessionId: 1  Cid: 0b28    Peb: 7ff7d00df000  ParentCid: 0f34
        DirBase: 1fb746000  ObjectTable: ffffc001db6b52c0  HandleCount:  34.
        Image: echoapp.exe
        VadRoot ffffe000800cf920 Vads 30 Clone 0 Private 135. Modified 8. Locked 0.
        DeviceMap ffffc001d83c6e80
        Token                             ffffc001cf5dc050
        ElapsedTime                       00:00:00.048
        UserTime                          00:00:00.000
        KernelTime                        00:00:00.000
        QuotaPoolUsage[PagedPool]         33824
        QuotaPoolUsage[NonPagedPool]      4464
        Working Set Sizes (now,min,max)  (681, 50, 345) (2724KB, 200KB, 1380KB)
        PeakWorkingSetSize                651
        VirtualSize                       16 Mb
        PeakVirtualSize                   16 Mb
        PageFaultCount                    686
        MemoryPriority                    BACKGROUND
        BasePriority                      8
        CommitCharge                      138

            THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
            IRP List:
                ffffe0007bc5be10: (0006,01f0) Flags: 00060a30  Mdl: 00000000
            Not impersonating
    ...
    ```

8.  与两个进程关联的记录的第一个线程地址。

    Cmd.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp.exe: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

9.  使用 **！线程**命令以显示有关当前线程的信息。

    ```dbgcmd
    0: kd>  !Thread
    THREAD ffffe000809a0880  Cid 0b28.1158  Teb: 00007ff7d00dd000 Win32Thread: 0000000000000000 RUNNING on processor 0
    IRP List:
        ffffe0007bc5be10: (0006,01f0) Flags: 00060a30  Mdl: 00000000
    Not impersonating
    DeviceMap                 ffffc001d83c6e80
    Owning Process            ffffe0008096c900       Image:         echoapp.exe
    Attached Process          N/A            Image:         N/A
    ...
    ```

    按预期运行，当前线程 echoapp.exe 与关联的线程，它是处于运行状态。

10. 使用 **！线程**命令以显示有关与 cmd.exe 进程关联线程的信息。 提供之前记录的线程地址。

    ```dbgcmd
    0: kd> !Thread ffffe0007cf34880
    THREAD ffffe0007cf34880  Cid 0f34.0f1c  Teb: 00007ff72dfae000 Win32Thread: 0000000000000000 WAIT: (UserRequest) UserMode Non-Alertable
        ffffe0008096c900  ProcessObject
    Not impersonating
    DeviceMap                 ffffc001d83c6e80
    Owning Process            ffffe0007bbde900       Image:         cmd.exe
    Attached Process          N/A            Image:         N/A
    Wait Start TickCount      4134621        Ticks: 0
    Context Switch Count      4056           IdealProcessor: 0             
    UserTime                  00:00:00.000
    KernelTime                00:00:01.421
    Win32 Start Address 0x00007ff72e9d6e20
    Stack Init ffffd0015551dc90 Current ffffd0015551d760
    Base ffffd0015551e000 Limit ffffd00155518000 Call 0
    Priority 14 BasePriority 8 UnusualBoost 3 ForegroundBoost 2 IoPriority 2 PagePriority 5
    Child-SP          RetAddr           : Args to Child                                                           : Call Site
    ffffd001`5551d7a0 fffff801`eed184fe : fffff801`eef81180 ffffe000`7cf34880 00000000`fffffffe 00000000`fffffffe : nt!KiSwapContext+0x76 [d:\9142\minkernel\ntos\ke\amd64\ctxswap.asm @ 109]
    ffffd001`5551d8e0 fffff801`eed17f79 : ffff03a5`ca56a3c8 000000de`b6a6e990 000000de`b6a6e990 00007ff7`d00df000 : nt!KiSwapThread+0x14e [d:\9142\minkernel\ntos\ke\thredsup.c @ 6347]
    ffffd001`5551d980 fffff801`eecea340 : ffffd001`5551da18 00000000`00000000 00000000`00000000 00000000`00000388 : nt!KiCommitThreadWait+0x129 [d:\9142\minkernel\ntos\ke\waitsup.c @ 619]
    ...
    ```

    此线程与 cmd.exe 相关联，处于等待状态。

11. 提供等待 CMD.exe 线程以将上下文更改为该等待线程的线程地址。

    ```dbgcmd
    0: kd> .Thread ffffe0007cf34880
    Implicit thread is now ffffe000`7cf34880
    ```

12. 使用**k**命令以查看调用堆栈与等待的线程关联。

    ```dbgcmd
    0: kd> k
      *** Stack trace for last set context - .thread/.cxr resets it
    # Child-SP          RetAddr           Call Site
    00 ffffd001`5551d7a0 fffff801`eed184fe nt!KiSwapContext+0x76 [d:\9142\minkernel\ntos\ke\amd64\ctxswap.asm @ 109]
    01 ffffd001`5551d8e0 fffff801`eed17f79 nt!KiSwapThread+0x14e [d:\9142\minkernel\ntos\ke\thredsup.c @ 6347]
    02 ffffd001`5551d980 fffff801`eecea340 nt!KiCommitThreadWait+0x129 [d:\9142\minkernel\ntos\ke\waitsup.c @ 619]
    03 ffffd001`5551da00 fffff801`ef02e642 nt!KeWaitForSingleObject+0x2c0 [d:\9142\minkernel\ntos\ke\wait.c @ 683]
    ...
    ```

    调用堆栈元素，如**KiCommitThreadWait**指示该线程不运行是正常。

**注意**  
有关线程和进程的详细信息，请参阅以下引用：

[线程和进程](threads-and-processes.md)

[更改上下文](changing-contexts.md)



## <a name="span-idsection10irqlregistersandendingthewindbgsessionspanspan-idsection10irqlregistersandendingthewindbgsessionspanspan-idsection10irqlregistersandendingthewindbgsessionspansection-10-irql-registers-and-ending-the-windbg-session"></a><span id="Section_10__IRQL__Registers_and_Ending_the_WinDbg_session"></span><span id="section_10__irql__registers_and_ending_the_windbg_session"></span><span id="SECTION_10__IRQL__REGISTERS_AND_ENDING_THE_WINDBG_SESSION"></span>第 10 部分：IRQL，寄存器并结束 WinDbg 会话

### <a name="span-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanviewing-the-saved-irql"></a><span id="IRQLRegistersMemory"></span><span id="irqlregistersmemory"></span><span id="IRQLREGISTERSMEMORY"></span>查看已保存的 IRQL

*在部分 10 中，将显示 irql，因此和 regsisters 的内容。*

**&lt;在主机系统**

中断请求级别 (IRQL) 用于管理的服务中断的优先级。 每个处理器都有线程可以提高或降低的 IRQL 设置。 中断的发生或以下处理器的 IRQL 设置被屏蔽并不会干扰当前操作。 中断的发生以上处理器的 IRQL 设置优先于当前操作。 [ **！ Irql** ](-irql.md)扩展当前的目标计算机的处理器上显示的中断请求级别 (IRQL)，在调试器中断发生之前。 当目标计算机进入调试器，IRQL 更改，但 IRQL 有效只是随着在调试器中断保存和显示通过 **！ irql**。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanspan-idviewingtheregistersspanspan-idviewingtheregistersspanviewing-the-registers"></a><span id="ViewingTheRegisters"></span><span id="viewingtheregisters"></span><span id="VIEWINGTHEREGISTERS"></span>查看寄存器

**&lt;在主机系统**

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

或者，您可以通过单击显示寄存器的内容**视图** &gt; **注册**。 有关详细信息请参阅[ **r （寄存器）**](r--registers-.md)。

逐句通过程序集语言代码执行和在其他情况下时，查看寄存器内容非常有用。 有关程序集语言反汇编的详细信息，请参阅[Annotated x86 反汇编](annotated-x86-disassembly.md)并[Annotated x64 反汇编](annotated-x64-disassembly.md)。

寄存器的内容的信息，请参阅[x86 体系结构](x86-architecture.md)并[x64 体系结构](x64-architecture.md)。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanspan-idendingthesessionspanending-the-windbg-session"></a><span id="EndingTheSession"></span><span id="endingthesession"></span><span id="ENDINGTHESESSION"></span>结束 WinDbg 会话

**&lt;在主机系统**

若要用户模式下调试会话结束，返回休眠模式下，调试器并设置目标应用程序再次运行，请输入**qd** （Quit 和分离） 命令。

确保并用**g**命令，以使目标计算机运行的代码，以便可以使用它。 它还建议清除任何断点，使用 * * bc \\* * *，以便目标计算机不会中断并尝试连接到主机计算机调试器。

```dbgcmd
0: kd> qd
```

有关详细信息，请参阅[结束调试会话在 WinDbg 中](ending-a-debugging-session-in-windbg.md)调试的参考文档中。

## <a name="span-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspansection-11-windows-debugging-resources"></a><span id="WindowsDebuggingResources"></span><span id="windowsdebuggingresources"></span><span id="WINDOWSDEBUGGINGRESOURCES"></span>第 11 节：Windows 调试资源


有关 Windows 调试提供了其他信息。 请注意，这些书籍将使用在其示例中，如 Windows Vista 的 Windows 的较旧版本，但要讨论的概念也适用于大多数版本的 Windows。

**丛书**

-   高级的 Windows 调试由 Mario Hewardt 和 Daniel Pravat

-   深入了解 Windows 调试：调试和跟踪策略通过 Tarik Soulami Windows® 中的实践指南

-   Mark E.Russinovich、 David A.Solomon 和 Alex Ionescu Windows 内部结构

**视频**

碎片整理工具显示 WinDbg 剧集 13 29 <https://channel9.msdn.com/Shows/Defrag-Tools>

**培训供应商：**

OSR <https://www.osr.com/>

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[标准调试技术](standard-debugging-techniques.md)

[专用的调试技术](specialized-debugging-techniques.md)

[Windows 调试入门](getting-started-with-windows-debugging.md)










