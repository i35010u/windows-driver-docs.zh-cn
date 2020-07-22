---
title: 调试 Windows 驱动程序-分步实验室（回显内核模式）
description: 此实验室引入了 WinDbg 内核调试器。 WinDbg 用于调试回显内核模式示例驱动程序代码。
ms.assetid: 3FBC3693-4288-42BA-B1E8-84DC2A9AFFD9
keywords:
- 调试实验室
- 循序渐进
- ECHO
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: a14d525f369aa573ae8bbddc8760000fc0526489
ms.sourcegitcommit: 3ec971f54122b77408433f7f1e59c467099fb4de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86873866"
---
# <a name="debug-windows-drivers---step-by-step-lab-echo-kernel-mode"></a>调试 Windows 驱动程序 - 分步实验室（Echo 内核模式）

此实验室引入了 WinDbg 内核调试器。 WinDbg 用于调试回显内核模式示例驱动程序代码。

## <a name="span-idlab_objectivesspanspan-idlab_objectivesspanspan-idlab_objectivesspanlab-objectives"></a><span id="Lab_objectives"></span><span id="lab_objectives"></span><span id="LAB_OBJECTIVES"></span>实验室目标

此实验室包括一些练习，其中引入了调试工具、讲授常见的调试命令、阐释了断点的使用，并演示了调试扩展的使用。

在此实验室中，使用实时内核调试连接来浏览以下内容：

- 使用 Windows 调试器命令
- 使用标准命令（调用堆栈、变量、线程、IRQL）
- 使用高级驱动程序调试命令（！命令）
- 使用符号
- 在实时调试中设置断点
- 查看调用堆栈
- 显示即插即用设备树
- 使用线程和进程上下文

**注意** 使用 Windows 调试器时，可以执行两种类型的调试：用户或内核模式调试。

*用户模式*-应用程序和子系统在计算机上以用户模式运行。 在用户模式下运行的进程在其自己的虚拟地址空间内执行此操作。 它们受到限制，无法直接访问系统的多个部分，包括系统硬件、未分配给其使用的内存，以及可能危及系统完整性的系统的其他部分。 由于在用户模式下运行的进程有效地与系统和其他用户模式进程隔离，因此它们不能干扰这些资源。

*内核模式*-内核模式是运行操作系统和特权程序的处理器访问模式。 内核模式代码有权访问系统的任何部分，并且不受限于用户模式代码。 它可以访问在用户模式或内核模式下运行的任何其他进程的任何部分。 许多核心操作系统功能和许多硬件设备驱动程序在内核模式下运行。

此实验室将重点介绍内核模式调试，就像用于调试多个设备驱动程序的方法一样。

此练习涉及在用户模式和内核模式调试过程中经常使用的调试命令。 本练习还介绍了用于内核模式调试的调试扩展（有时称为 "！命令"）。

## <a name="span-idlab_setupspanspan-idlab_setupspanspan-idlab_setupspanlab-setup"></a><span id="Lab_setup"></span><span id="lab_setup"></span><span id="LAB_SETUP"></span>实验室设置

你将需要以下硬件才能完成实验室。

- 运行 Windows 10 的便携式计算机或台式计算机（主机）
- 运行 Windows 10 的便携式计算机或台式计算机（目标）
- 用于连接两台电脑的网络集线器/路由器和网络电缆
- 访问 internet 以下载符号文件

你将需要以下软件才能完成实验室。

- Visual Studio 
- 适用于 Windows 10 的 Windows 软件开发工具包 (SDK)
- 适用于 Windows 10 的 windows 驱动程序工具包（WDK）
- 适用于 Windows 10 的示例回显驱动程序

实验室有以下11个部分。

- [第1节：连接到内核模式 WinDbg 会话](#connectto)
- [第2部分：内核模式调试命令和技术](#kernelmodedebuggingcommandsandtechniques)
- [第3部分：下载并构建 KMDF Echo 驱动程序](#download)
- [第4部分：在目标系统上安装 KMDF Echo 驱动程序示例](#install)
- [第5节：使用 WinDbg 显示有关驱动程序的信息](#usewindbgtodisplayinformation)
- [第6部分：显示即插即用设备树信息](#displayingtheplugandplaydevicetree)
- [第7部分：处理断点和源代码](#workingwithbreakpoints)
- [第8节：查看变量和调用堆栈](#viewingvariables)
- [第9部分：显示进程和线程](#displayingprocessesandthreads)
- [第10部分： IRQL、注册和结束 WinDbg 会话](#irqlregistersmemory)
- [第11节： Windows 调试资源](#windowsdebuggingresources)

## <a name="span-idconnecttospanspan-idconnecttospansection-1-connect-to-a-kernel-mode-windbg-session"></a><span id="connectto"></span><span id="CONNECTTO"></span>第1节：连接到内核模式 WinDbg 会话

*在第1部分中，你将在主机和目标系统上配置网络调试。*

此实验室中的电脑需要配置为使用以太网网络连接进行内核调试。

此实验室使用两台电脑。 Windows 调试器在*主机*系统上运行，KMDF Echo 驱动程序在*目标*系统上运行。

 使用网络集线器/路由器和网络电缆连接两台 Pc。

![使用双箭头连接的两台电脑](images/debuglab-image-targethostdrawing1.png)

若要使用内核模式应用程序并使用 WinDbg，建议使用 KDNET over 以太网传输。 有关如何使用以太网传输协议的信息，请参阅[使用 WinDbg 入门（内核模式）](getting-started-with-windbg--kernel-mode-.md)。 有关设置目标计算机的详细信息，请参阅[为手动驱动程序部署准备计算机](https://docs.microsoft.com/windows-hardware/drivers)和[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

### <a name="span-idconfigure__kernel_mode_debugging_using_ethernetspanspan-idconfigure__kernel_mode_debugging_using_ethernetspanspan-idconfigure__kernel_mode_debugging_using_ethernetspanconfigure-kernelmode-debugging-using-ethernet"></a><span id="Configure__kernel_mode_debugging_using_ethernet"></span><span id="configure__kernel_mode_debugging_using_ethernet"></span><span id="CONFIGURE__KERNEL_MODE_DEBUGGING_USING_ETHERNET"></span>使用以太网配置内核-模式调试

若要在目标系统上启用内核模式调试，请执行以下步骤。

**&lt;-在主机系统上**

1. 在主机系统上打开命令提示符，然后键入**ipconfig**以确定其 IP 地址。

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

2. 记录主机系统的 IP 地址：\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

**-&gt;在目标系统上**

3. 在目标系统上打开命令提示符，并使用**ping**命令确认两个系统之间的网络连接。 使用所记录主机系统的实际 IP 地址，而不是示例输出中所示的169.182.1.1。

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

通过完成以下步骤，在目标系统上启用内核模式调试。

> [!IMPORTANT]
> 使用 BCDEdit 更改启动信息之前，您可能需要在测试电脑上暂时挂起 Windows 安全功能，例如 BitLocker 和安全启动。
> 当安全功能处于禁用状态时，在测试完成后重新启用这些安全功能，并对测试 PC 进行适当的管理。

1. 在目标计算机上，以管理员身份打开“命令提示符”窗口。 输入此命令以启用调试。

    ```console
    C:\> bcdedit /set {default} DEBUG YES
    ```

2. 键入以下命令以启用测试签名。

    ```console
    C:\> bcdedit /set TESTSIGNING ON 
    ```


3. 键入此命令可设置主机系统的 IP 地址。 使用之前记录的主机系统的 IP 地址，而不是显示的 IP 地址。

    ```console
    C:\> bcdedit /dbgsettings net hostip:192.168.1.1 port:50000 key:1.2.3.4
    ```

**警告** 若要提高连接的安全性并降低随机客户端调试器连接请求的风险，请考虑使用自动生成的随机密钥。 有关详细信息，请参阅[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)。

4. 键入以下命令，确认已正确设置 dbgsettings。

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

如果收到来自防火墙的弹出消息，并且想要使用调试器，请选中**所有三**个框。

![windows 安全警报-windows 防火墙阻止了此应用的某些功能 ](images/debuglab-image-firewall-dialog-box.png)

**&lt;-在主机系统上**

1. 在主计算机上，以管理员身份打开命令提示符窗口。 我们将使用 Windows 驱动程序工具包（WDK）中的 x64 版本的 WinDbg.exe，该版本作为 Windows 工具包安装的一部分进行安装。 默认情况下，它位于此处。

    ```console
    C:\> Cd C:\Program Files(x86)\Windows Kits\10\Debuggers\x64 
    ```

> [!NOTE]
> 此实验室假定两台 Pc 同时在目标和主机上运行64位版本的 Windows。
> 如果不是这种情况，最好的方法是在目标正在运行的主机上运行相同的工具 "位数"。
例如，如果目标运行的是32位 Windows，请在主机上运行调试器的32版本。 有关详细信息，请参阅[选择32位或64位调试工具](choosing-a-32-bit-or-64-bit-debugger-package.md)。
>

2. 使用以下命令通过远程用户调试启动 WinDbg。 此键和端口的值与我们以前在目标上使用 BCDEdit 时所设置的值匹配。

    ```console
    WinDbg –k net:port=50000,key=1.2.3.4
    ```

**-&gt;在目标系统上**

重新启动目标系统。

**&lt;-在主机系统上**

在一分钟或两分钟内，调试输出应显示在主机系统上。

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

调试器命令窗口是 WinDbg 的主调试信息窗口。 您可以在此窗口中输入调试器命令并查看命令输出。

调试器命令窗口拆分为两个窗格。 您可以在窗口底部的小窗格（命令条目窗格）中键入命令，然后在窗口顶部更大的窗格中查看命令输出。

在 "命令项" 窗格中，使用向上键和向下键滚动浏览命令历史记录。 显示命令时，你可以对其进行编辑或按**enter**运行该命令。

## <a name="span-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspanspan-idkernelmodedebuggingcommandsandtechniquesspansection-2-kernel-mode-debugging-commands-and-techniques"></a><span id="KernelModeDebuggingCommandsAndTechniques"></span><span id="kernelmodedebuggingcommandsandtechniques"></span><span id="KERNELMODEDEBUGGINGCOMMANDSANDTECHNIQUES"></span>第2部分：内核模式调试命令和技术


*在第2部分中，你将使用 "调试" 命令显示有关目标系统的信息。*

**&lt;-在主机系统上**

**使用启用调试器标记语言（DML）。优先使用 \_ DML**

某些调试命令使用调试器标记语言显示文本，您可以单击该语言来快速收集详细信息。

1. 使用 WinDBg 中的 Ctrl + Break （滚动锁定）来中断目标系统上运行的代码。 目标系统可能需要一些时间才能响应。

![显示实时内核连接的命令窗口输出的 windows 调试器](images/debuglab-image-winddbg-hh.png)


2. 键入以下命令，在调试器中启用 DML 命令窗口。

```dbgcmd
0: kd> .prefer_dml 1
DML versions of commands on by default
```

**使用 hh 获取帮助**

您可以使用**hh**命令访问 reference 命令帮助。

3. 键入以下命令以查看的命令参考帮助 **。首选 \_ dml**。

```dbgcmd
0: kd> .hh .prefer_dml
```

调试器帮助文件将显示的帮助 **。 \_ **

![调试器帮助应用程序，显示的帮助。首选 \- dml 命令](images/debuglab-image-prefer-dml-help.png)

**显示目标系统上的 Windows 版本**

5. 在 WinDbg 窗口中键入[**vertarget （显示目标计算机版本）**](vertarget--show-target-computer-version-.md)命令，以显示目标系统上的详细版本信息。

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

6. 您可以通过在 WinDbg 窗口中键入 " [**lm （列表加载的模块）**](lm--list-loaded-modules-.md) " 命令，来验证是否正在使用正确的内核模式进程。

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

**注意** 已省略的输出用 "...。 "。



7. 若要请求有关特定模块的详细信息，请使用 "v （详细）" 选项，如下所示。

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

8. 由于我们尚未设置符号路径和加载的符号，因此在调试器中提供了有限的信息。

## <a name="span-iddownloadspanspan-iddownloadspanspan-iddownloadspansection-3-download-and-build-the-kmdf-echo-driver"></a><span id="Download"></span><span id="download"></span><span id="DOWNLOAD"></span>第3部分：下载并构建 KMDF echo 驱动程序

*在第3部分中，你将下载并构建 KMDF echo 驱动程序。*

通常，使用 WinDbg 时，将使用自己的驱动程序代码。 若要熟悉 WinDbg 操作，请使用 KMDF 模板 "Echo" 示例驱动程序。 使用可用的源代码，还可以更容易地理解 WinDbg 中显示的信息。 此外，此示例还可用于说明如何单步执行本机内核模式代码。 此方法对于调试复杂的内核模式代码问题非常有用。

若要下载并构建 Echo 示例音频驱动程序，请执行以下步骤。

1.  **从 GitHub 下载并提取 KMDF Echo 示例**

    可在 GitHub 中使用浏览器查看回显示例：

    [https://github.com/Microsoft/Windows-driver-samples/tree/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf](https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md)

    可在此处阅读有关示例的内容：

    <https://github.com/Microsoft/Windows-driver-samples/blob/97cf5197cf5b882b2c689d8dc2b555f2edf8f418/general/echo/kmdf/ReadMe.md>

    你可以在此处浏览所有 Windows 驱动程序示例：

    <https://github.com/Microsoft/Windows-driver-samples>

    KMDF Echo 示例位于常规文件夹中。

    ![github windows-驱动程序-示例突出显示 "常规" 文件夹和 "下载 zip" 按钮](images/debuglab-image-github.png)

    a. 此实验室演示如何在一个 zip 文件中下载驱动程序示例。

    <https://github.com/Microsoft/Windows-driver-samples/archive/master.zip>

    b. 将 master.zip 文件下载到本地硬盘驱动器。

    c. 右键单击*Windows-driver-samples-master.zip*，然后选择 "**全部提取**"。 指定一个新文件夹，或浏览到将存储所提取文件的现有文件夹。 例如，你可以将*C： \\ DriverSamples \\ *指定为要将文件提取到的新文件夹。

    d. 提取文件后，导航到以下子文件夹。

    *C： \\ DriverSamples \\ 常规 \\ 回显 \\ kmdf*

2.  **在 Visual Studio 中打开驱动程序解决方案**

    在 Microsoft Visual Studio 中，单击 "**文件**" " &gt; **打开** &gt; **项目/解决方案 ...** "，然后导航到包含所提取文件的文件夹（例如， *C： \\ DriverSamples \\ 常规 \\ echo \\ kmdf*）。 双击 " *kmdfecho* " 解决方案文件以将其打开。

    在 Visual Studio 中，找到解决方案资源管理器。 （如果尚未打开，请从 "**视图**" 菜单中选择 "**解决方案资源管理器**"。）在解决方案资源管理器中，可以看到一个包含三个项目的解决方案。

    ![带有从 kmdfecho 项目加载的设备 .c 文件的 visual studio](images/debuglab-image-echo-visual-studio.png)

3.  **设置示例的配置和平台**

    在解决方案资源管理器中，右键单击 "**解决方案 ' kmdfecho ' （3个项目）"**，然后选择 " **Configuration Manager**"。 请确保三个项目的配置和平台设置相同。 默认情况下，将配置设置为 "Win10 调试"，并将所有项目的平台设置为 "Win64"。 如果对一个项目进行任何配置和/或平台更改，则必须为其余三个项目进行相同的更改。

4.  **设置运行时库**

    设置运行库-打开回显驱动程序的属性页，并找到**c/c + +** &gt; **代码生成**。  将运行库从 DLL 版本更改为非 DLL 版本。 如果没有此设置，则必须单独将 MSVC 运行时安装到目标计算机上。

    ![显示运行时库设置的回响属性页](images/debuglab-image-echoapp-properties.png)

5.  **检查驱动程序签名**

    此外，在驱动程序的属性中，请确保将**驱动程序签名** &gt; **模式**设置为 "测试签名"。 这是必需的，因为 Windows 要求对驱动程序进行签名。

    ![显示签名模式设置的回响属性页](images/debuglab-image-echoapp-driver-signing.png)

6.  **使用 Visual Studio 生成示例**

    在 Visual Studio 中，单击 "**生成**" "生成 &gt; **解决方案**"。

    如果一切顺利，生成窗口应显示一条消息，指示所有三个项目的生成均已成功。

7.  **找到生成的驱动程序文件**

    在 "文件资源管理器" 中，导航到包含示例提取的文件的文件夹。 例如，如果是前面指定的文件夹，请导航到*C： \\ DriverSamples \\ 常规 \\ echo \\ kmdf*。 在该文件夹中，编译的驱动程序文件的位置根据你在**Configuration Manager**中选择的配置和平台设置而有所不同。 例如，如果将默认设置保持不变，则已编译的驱动程序文件将保存到一个名为* \\ x64 \\ 调试*的名为 "64 位，调试生成" 的文件夹中。

    导航到包含 Autosync 驱动程序的生成文件的文件夹：

    *C： \\DriverSamples \\ 常规 \\ echo \\ kmdf \\ driver \\ AutoSync \\ x64 \\ 调试*。 

    该文件夹应包含以下文件：

    | 文件     | 说明                                                                       |
    |----------|-----------------------------------------------------------------------------------|
    | Echo.sys | 驱动程序文件。                                                                  |
    | 回显 .inf | 一个信息（INF）文件，其中包含安装驱动程序所需的信息。 |

    此外，还生成 echoapp.exe 文件，该文件应位于以下位置： *C： \\ DriverSamples \\ 常规 \\ echo \\ kmdf \\ exe \\ x64 \\ 调试*

    | 文件        | 说明                                                                       |
    |-------------|-----------------------------------------------------------------------------------|
    | EchoApp.exe | 与 echo.sys 驱动程序通信的命令提示符可执行文件测试文件。 |     

8.  找到 USB 拇指驱动器或设置网络共享，以将构建的驱动程序文件和测试 EchoApp 从主机复制到目标系统。

在下一部分中，你将代码复制到目标系统，然后安装并测试驱动程序。

## <a name="span-idinstallspanspan-idinstallspanspan-idinstallspansection-4-install-the-kmdf-echo-driver-sample-on-the-target-system"></a><span id="Install"></span><span id="install"></span><span id="INSTALL"></span>第4部分：在目标系统上安装 KMDF echo 驱动程序示例

*在第4部分中，你将使用 devcon 安装 echo 示例驱动程序。*

安装驱动程序的计算机称为*目标计算机*或*测试计算机*。 通常，这是与你开发和构建驱动程序包的计算机不同的计算机。 开发和构建驱动程序的计算机称为 "*主机*"。

将驱动程序包移动到目标计算机并安装驱动程序的过程称为 "*部署*驱动程序"。

在部署测试签名驱动程序之前，必须通过启用测试签名来准备目标计算机。 还需要在 WDK 安装中找到 DevCon 工具，并将其复制到目标系统。

若要在目标系统上安装驱动程序，请执行以下步骤。

**-&gt;在目标系统上**

**启用测试签名驱动程序**

启用运行测试签名驱动程序的功能：

a. 打开 Windows 设置。

b. 在 "更新和安全性" 中，选择 "**恢复**"。

c. 在 "高级启动" 下，单击 "**立即重新启动**"。

d. 重新启动计算机时，请选择 "**启动选项**"。 在 Windows 10 中， **Troubleshoot**选择 "  >  **高级选项**  >  " "**启动设置**故障排除"，然后单击 "重新启动" 按钮。

e. 按**F7**键，选择 "禁用驱动程序签名强制"。

f. 重新启动目标计算机。

**&lt;-在主机系统上**

导航到 WDK 安装中的 "工具" 文件夹，并找到 DevCon 工具。 例如，在以下文件夹中查看：

*C:\\Program Files (x86)\\Windows Kits\\10\\Tools\\x64\\devcon.exe*

在目标上为生成的驱动程序包创建一个文件夹（例如， *C： \\ EchoDriver*）。 将 devcon.exe 复制到目标系统。 在主机系统上找到 .cer 证书，该证书位于主计算机上包含生成的驱动程序文件的文件夹中的相同文件夹中。 复制主机计算机上前面介绍的生成驱动程序中的所有文件，并将它们保存到你在目标计算机上创建的同一个文件夹中。

**-&gt;在目标系统上**

在目标计算机上，右键单击证书文件，然后单击 "**安装**"，然后按照提示安装测试证书。

如果需要有关设置目标计算机的更详细说明，请参阅为[手动驱动程序部署准备计算机](../develop/preparing-a-computer-for-manual-driver-deployment.md)。

**-&gt;在目标系统上**

**安装驱动程序**

下面的说明演示了如何安装和测试示例驱动程序。 以下是将用于安装驱动程序的 devcon 工具的常规语法：

devcon install &lt;INF 文件&gt; &lt;硬件 ID&gt;

安装此驱动程序所需的 INF 文件为 " *echo*"。 Inf 文件包含用于安装*echo.sys*的硬件 ID。 对于 echo 示例，硬件 ID 是**根 \\ echo**。

在目标计算机上，以管理员身份打开“命令提示符”窗口。 导航到驱动程序包文件夹，然后输入以下命令：

**devcon 安装 echo 根目录 \\回显**如果收到有关无法识别*devcon*的错误消息，请尝试将路径添加到*devcon*工具。 例如，如果将该文件复制到名为*C： \\ Tools*的文件夹，请尝试使用以下命令：

**c： \\ 工具 \\ devcon install echo root \\ echo**将出现一个对话框，指示测试驱动程序是未签名的驱动程序。 单击“仍然安装此驱动程序”以继续。

![windows 安全警告-windows 无法验证此驱动程序软件的发布者](images/debuglab-image-install-security-warning.png)

>[!TIP]
> 如果安装有任何问题，请查看以下文件以了解详细信息。
`%windir%\inf\setupapi.dev.log`

成功安装示例驱动程序后，就可以对其进行测试了。

**查看设备管理器中的驱动程序**

在目标计算机上的命令提示符窗口中，输入**devmgmt.msc** open 设备管理器。 在设备管理器的 "视图" 菜单上，选择 "设备（按类型）"。 在设备树中，找到示例设备节点中的 "*示例 WDF 回显驱动程序*"。

![突出显示了示例 wdf 回显驱动程序的设备管理器树](images/debuglab-image-device-manager-echo.png)

**测试驱动程序**

键入**echoapp**以启动测试回显应用，以确认该驱动程序是否正常运行。

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

## <a name="span-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspanspan-idusewindbgtodisplayinformationspansection-5-use-windbg-to-display-information-about-the-driver"></a><span id="UseWinDbgToDisplayInformation"></span><span id="usewindbgtodisplayinformation"></span><span id="USEWINDBGTODISPLAYINFORMATION"></span>第5节：使用 WinDbg 显示有关驱动程序的信息

*在第5部分中，您将设置符号路径并使用内核调试器命令显示有关 KMDF echo 示例驱动程序的信息。*

通过执行以下步骤来查看有关驱动程序的信息。

**&lt;-在主机系统上**

1.  如果关闭了调试器，请在管理员命令提示符窗口中使用以下命令重新打开它。

    ```dbgcmd
    WinDbg -k net:port=50000,key=1.2.3.4
    ```

2.  使用 Ctrl + Break （滚动锁定）进入目标系统上运行的代码。

**设置符号路径**

1.  若要在 WinDbg 环境中将符号路径设置为 Microsoft 符号服务器，请使用**symfix**命令。

    ```dbgcmd
    0: kd> .symfix
    ```

2.  若要添加您的本地符号位置以使用您的本地符号，请使用 **. sympath +** 和 then **/f**添加该路径。

    ```dbgcmd
    0: kd> .sympath+ C:\DriverSamples\general\echo\kmdf
    0: kd> .reload /f
    ```

    **注意** 带有 **/f** force 选项的**reload.sql**命令将删除指定模块的所有符号信息，并重新加载符号。 在某些情况下，此命令还会重新加载或卸载模块本身。



**注意** 您必须加载适当的符号才能使用 WinDbg 提供的高级功能。 如果未正确配置符号，则在尝试使用依赖于符号的功能时，你将收到一条消息，指示符号不可用。

```dbgcmd
0:000> dv
Unable to enumerate locals, HRESULT 0x80004005
Private symbols (symbols.pri) are required for locals.
Type “.hh dbgerr005” for details.
```



**注意**  
**符号服务器**

有多种方法可用于处理符号。 在许多情况下，可以将 PC 配置为从 Microsoft 在需要时提供的符号服务器访问符号。 本演练假定将使用此方法。 如果你的环境中的符号位于不同的位置，请修改这些步骤以使用该位置。 有关其他信息，请参阅[符号存储和符号服务器](symbol-stores-and-symbol-servers.md)。



**注意**  
**了解源代码符号要求**

若要执行源调试，必须生成已选中（调试）的二进制文件版本。 编译器将创建符号文件（.pdb 文件）。 这些符号文件将显示调试器与源行的对应关系。 实际的源文件本身还必须可供调试器访问。

符号文件不包含源代码的文本。 对于调试，最好是链接器不优化代码。 如果代码已经过优化，则源调试和对本地变量的访问更难，有时可能几乎不可能。 如果在查看本地变量或源行时遇到问题，请设置以下生成选项：

```console
set COMPILE_DEBUG=1
set ENABLE_OPTIMIZER=0
```



1. 在调试器的 "命令" 区域中键入以下内容以显示有关 echo 驱动程序的信息：

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

   有关信息，请参阅[**lm**](lm--list-loaded-modules-.md)。

2. 由于我们前面设置了更喜欢的 \_ dml = 1，因此输出的某些元素是可单击的热链接。 单击 "调试输出" 中的 "*浏览所有全局符号" 链接*，以显示以字母 "a" 开头的项符号的相关信息。

   ```dbgcmd
   0: kd> x /D Echo!a*
   ```

3. 事实证明，echo 示例不包含以字母 "a" 开头的任何符号，因此请键入 `x ECHO!Echo*` 以显示与 echo 驱动程序相关联的所有与 echo 驱动程序相关联的信息。

   ```dbgcmd
   0: kd> x ECHO!Echo*
   fffff801`0bf95690 ECHO!EchoEvtIoQueueContextDestroy (void *)
   fffff801`0bf95000 ECHO!EchoEvtDeviceSelfManagedIoStart (struct WDFDEVICE__ *)
   fffff801`0bf95ac0 ECHO!EchoEvtTimerFunc (struct WDFTIMER__ *)
   fffff801`0bf9b120 ECHO!EchoEvtDeviceSelfManagedIoSuspend (struct WDFDEVICE__ *)
   ...
   ```

   有关信息，请参阅[**x （检查符号）**](x--examine-symbols-.md)。

4. **！ Lmi**扩展显示有关模块的详细信息。 键入 **！ lmi echo**。 输出应类似于下面所示的文本。

   ```dbgcmd
   0: kd> !lmi echo
   Loaded Module Info: [echo] 
            Module: ECHO
      Base Address: fffff8010bf94000
        Image Name: ECHO.sys
   … 
   ```

5. 使用 **！ dh**扩展显示标头信息，如下所示。

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

   键入以下项以更改默认调试位掩码，以便从目标系统中的所有调试消息都显示在调试器中。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0xFFFFFFFF
   ```

   当使用0xFFFFFFFF 的掩码时，某些驱动程序将显示其他信息。 如果要减少显示的信息量，请将掩码设置为0x00000000。

   ```dbgcmd
   0: kd> ed nt!Kd_DEFAULT_MASK  0x00000000
   ```

   使用 dd 命令显示 "确认掩码" 设置为显示所有调试器消息。 

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


## <a name="span-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespanspan-iddisplayingtheplugandplaydevicetreespansection-6-displaying-plug-and-play-device-tree-information"></a><span id="DisplayingThePlugAndPlayDeviceTree"></span><span id="displayingtheplugandplaydevicetree"></span><span id="DISPLAYINGTHEPLUGANDPLAYDEVICETREE"></span>第6部分：显示即插即用设备树信息

*在第6部分中，将显示有关 echo 示例设备驱动程序以及它在即插即用设备树中的位置的信息。*

有关故障排除的详细信息，请查看即插即用设备树中的设备驱动程序。 例如，如果设备驱动程序不在设备树中，则设备驱动程序的安装可能会出现问题。

有关设备节点调试扩展的详细信息，请参阅[**！ devnode**](-devnode.md)。

**&lt;-在主机系统上**

1. 若要查看即插即用设备树中的所有设备节点，请输入 **！ devnode 0 1**命令。

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

2. 使用 Ctrl + F 在生成的输出中搜索，以查找设备驱动程序的名称， *echo*。

   ![显示要搜索的字词回显的 "查找" 对话框](images/debuglab-image-find-dialog.png)

3. 应加载 echo 设备驱动程序。 使用 **！ devnode 0 1 echo**命令显示与回显设备驱动程序关联的即插即用信息，如下所示。

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

4. 前一个命令中显示的输出包含与驱动程序的正在运行的实例关联的 PDO，在此示例中为*0xffffe0007b71a960*。 输入 **！ devobj**<em> &lt; PDO address &gt; </em>命令以显示与 echo 设备驱动程序关联即插即用信息。 使用 **！ devnode**在你的电脑上显示的 PDO 地址，而不是此处显示的地址。

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

5. **！ Devnode 0 1**命令中显示的输出包含与驱动程序的正在运行的实例关联的 PDO 地址，在此示例中为*0xffffe0007b71a960*。 输入 **！ devstack**<em> &lt; PDO address &gt; </em>命令以显示与设备驱动程序相关即插即用信息。 使用 **！ devnode**在你的电脑上显示的 PDO 地址，而不是以下显示的地址。

   ```dbgcmd
   0: kd> !devstack 0xffffe0007b71a960
     !DevObj           !DrvObj            !DevExt           ObjectName
     ffffe000801fee20  \Driver\ECHO       ffffe0007f72eff0  
   > ffffe0007b71a960  \Driver\PnpManager 00000000  0000000e
   !DevNode ffffe0007b71a630 :
     DeviceInst is "ROOT\SAMPLE\0000"
     ServiceName is "ECHO"
   ```

输出显示我们有一个相当简单的设备驱动程序堆栈。 Echo 驱动程序是 PnPManager 节点的子节点。 PnPManager 是根节点。

\Driver\ECHO

\Driver\PnpManager

此图显示了更复杂的设备节点树。

![包含大约20个节点的设备节点树](images/debuglab-image-device-node-tree.png)

**注意** 有关更复杂的驱动程序堆栈的详细信息，请参阅[驱动程序堆栈](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/driver-stacks)和[设备节点和设备堆栈](https://docs.microsoft.com/windows-hardware/drivers/gettingstarted/device-nodes-and-device-stacks)。

## <a name="span-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspanspan-idworkingwithbreakpointsspansection-7-working-with-breakpoints-and-source-code"></a><span id="WorkingWithBreakpoints"></span><span id="workingwithbreakpoints"></span><span id="WORKINGWITHBREAKPOINTS"></span>第7部分：使用断点和源代码

*在第7部分中，您将通过内核模式源代码设置断点和单步执行。*

**注意**  
**使用命令设置断点**

为了能够逐步执行代码并检查变量的值，我们需要启用断点并设置源代码的路径。

断点用于在特定代码行处停止执行代码。 然后，可以从该点开始前进，以调试该代码的特定部分。

若要使用调试命令设置断点，请使用下列**b**命令之一。

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
<td align="left"><p>设置符号的断点。 此命令将适当地使用 bu 或 bp，并允许使用通配符 * 来设置每个匹配的符号（如类中的所有方法）上的断点。</p></td>
</tr>
</tbody>
</table>

有关详细信息，请参阅调试参考文档[中的 WinDbg 中的源代码调试](source-window.md)。

**&lt;-在主机系统上**

1.  使用 WinDbg UI 确认**Debug** &gt; 在当前 WinDbg 会话中启用了 "调试**源" 模式**。

2.  键入以下命令，将本地代码位置添加到源路径。

    ```dbgcmd
    .srcpath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

3.  键入以下命令，将本地符号位置添加到符号路径中。

    ```dbgcmd
    .sympath+ C:\DriverSamples\KMDF_Echo_Sample\driver\AutoSync
    ```

4.  我们将使用**x**命令来检查与 echo 驱动程序关联的符号，以确定用于该断点的函数名称。 我们可以使用通配符或 Ctrl + F 来查找**DeviceAdd**函数名称。

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

    以上输出显示了回显驱动程序的**DeviceAdd**方法为*echo！EchoEvtDeviceAdd*。

    另外，我们还可以查看源代码，为断点找到所需的函数名称。

5.  使用**bm.exe**命令设置断点，使用驱动程序名称，后跟要设置断点的函数名称（例如**AddDevice**），用感叹号分隔。 我们将使用**AddDevice**来监视正在加载的驱动程序。

    ```dbgcmd
    0: kd> bm ECHO!EchoEvtDeviceAdd
      1: fffff801`0bf9b1c0 @!"ECHO!EchoEvtDeviceAdd"
    ```

    **注意**  
    您可以结合使用不同语法和设置变量，如 &lt; module &gt; ！ &lt;symbol &gt; 、 &lt; class &gt; ：： &lt; 方法 &gt; 、" &lt; file .cpp &gt; ： &lt; 行号 &gt; "，或跳过次数 &lt; 条件 &gt; &lt; \# &gt; 。 有关详细信息，请参阅[WinDbg 和其他 Windows 调试器中的条件断点](setting-a-conditional-breakpoint.md)。



6.  列出当前断点以确认是否通过键入**bl**命令设置了断点。

    ```dbgcmd
    0: kd> bl
    1 e fffff801`0bf9b1c0     0001 (0001) ECHO!EchoEvtDeviceAdd
    ```

    上面显示的输出中的 "e" 表示启用了断点号1。

7.  在目标系统上重新启动代码执行，方法是键入 "**开始**" 命令**g**。

8.  **-&gt;在目标系统上**

    在 Windows 中，使用图标或输入**mmc devmgmt.msc**打开**设备管理器**。 在设备管理器中，展开 "**示例**" 节点。

9.  右键单击 "KMDF Echo 驱动程序" 条目，然后从菜单中选择 "**禁用**"。

10. 再次右键单击 "KMDF Echo 驱动程序" 条目，然后从菜单中选择 "**启用**"。

11. **&lt;-在主机系统上**

    如果启用了驱动程序，则应激发[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)调试断点，并且应停止目标系统上的驱动程序代码的执行。 命中断点时，应在*AddDevice*例程开始时停止执行。 调试命令输出将显示 "命中断点 1"。

    ![显示示例代码局部变量和命令窗口的 windbg](images/debuglab-image-breakpoint-echo-deviceadd.png)

12. 键入**p**命令或按 F10 逐行逐行执行代码，直到到达[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的以下结尾。 将突出显示大括号字符 "}"。

    ![显示 adddevice 例程开头突出显示的大括号字符的代码窗口](images/debuglab-image-breakpoint-end-deviceadd.png)

13. 在下一部分中，我们将在执行 DeviceAdd 代码后检查变量的状态。

**注意**  
**修改断点状态**

您可以使用以下命令修改现有断点：

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



此外，还可以通过单击**edit** &gt; "在 WinDbg 中编辑**断点**" 来修改断点。 请注意，"断点" 对话框仅适用于现有的断点。 必须从命令行设置新断点。



**注意**  
**设置内存访问断点**

还可以设置在访问内存位置时激发的断点。 使用以下语法，使用 " **ba** （访问时中断）" 命令。

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
<td align="left"><p>execute （当 CPU 从地址提取指令时）</p></td>
</tr>
<tr class="even">
<td align="left"><p>r</p></td>
<td align="left"><p>读/写（CPU 读取或写入地址时）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>w</p></td>
<td align="left"><p>写入（CPU 写入地址时）</p></td>
</tr>
</tbody>
</table>



请注意，在任何给定的时间，只能设置四个数据断点，并由您确保正确对齐数据或不触发断点（单词必须以2为界限的地址结束），dword 必须可被4整除，并 quadwords 0 或8。

例如，若要在特定内存地址上设置读/写断点，可以使用如下所示的命令。

```dbgcmd
ba r 4 0x0003f7bf0
```



**注意**  
**单步执行调试器中的代码命令窗口**

以下命令可用于单步执行代码（使用括号中显示的关联键盘短切削）。

-   中断（Ctrl + Break）-只要系统正在运行且与 WinDbg 通信，则此命令将中断系统（内核调试器中的序列为 Ctrl + C）。

-   "运行到光标处" （F7 或 Ctrl + F10）–将光标放在要中断执行的源或反汇编窗口中，然后按 F7;代码执行将运行到该点。 请注意，如果代码执行流未到达光标指示的点（不执行 IF 语句），则 WinDbg 不会中断，因为代码执行过程不会到达指示的点。

-   运行（F5）–直到遇到断点或发生错误检查等事件时运行。

-   逐过程执行（F10）–此命令可使代码执行一次一条语句或一个指令。 如果遇到调用，代码执行将通过调用而不输入被调用的例程。 （如果编程语言为 C 或 c + +，WinDbg 为源模式，则可以使用**调试** &gt; 来打开或关闭源模式**源模式**）。

-   单步执行（F11）–此命令类似于 "逐过程"，不同之处在于执行调用的操作进入被调用例程。

-   跳出（Shift + F11）-此命令将执行运行并从当前例程（位于调用堆栈中的当前位置）中退出。 如果你已看到足够的例程，这会很有用。



有关详细信息，请参阅调试参考文档[中的 WinDbg 中的源代码调试](source-window.md)。

## <a name="span-idviewingvariablesspanspan-idviewingvariablesspanspan-idviewingvariablesspansection-8-viewing-variables-and-call-stacks"></a><span id="ViewingVariables"></span><span id="viewingvariables"></span><span id="VIEWINGVARIABLES"></span>第8节：查看变量和调用堆栈

*在第8节中，您将显示有关变量和调用堆栈的信息。*

此实验室假设你使用前面所述的过程在[*AddDevice*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程处停止。 若要在此处查看输出显示内容，请根据需要重复上述步骤。

**&lt;-在主机系统上**

**显示变量**

使用 "**查看** &gt; **本地**" 菜单项可显示局部变量。

![windbg 本地变量窗口](images/debuglab-image-display-variables.png)

**全局变量**

您可以通过键入来找到全局变量地址的位置 *？ &lt;变量名称 &gt; *。

**局部变量**

您可以通过键入**dv**命令显示给定帧的所有局部变量的名称和值。

```dbgcmd
0: kd> dv
         Driver = 0x00001fff`7ff9c838
     DeviceInit = 0xffffd001`51978190
         status = 0n0
```

**调用堆栈**

**注意**  
调用堆栈是已导致程序计数器当前位置的函数调用的链。 调用堆栈上的 top 函数是当前函数，下一个函数是调用当前函数的函数，依此类推。

若要显示调用堆栈，请使用 k \* 命令。

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





**&lt;-在主机系统上**

1. 如果要保留可用的调用堆栈，可以单击 "**查看** &gt; **调用堆栈**" 以查看它。 单击窗口顶部的列可以切换其他信息的显示。

![windbg 显示 "调用堆栈" 窗口](images/debuglab-image-display-callstacks.png)

2. 使用**kn**命令可在调试中断状态下的示例适配器代码时显示调用堆栈。

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

调用堆栈显示调用的内核（nt）即插即用代码（PnP）中，该代码调用了驱动程序框架代码（WDF），后者随后称为 echo driver **DeviceAdd**函数。

## <a name="span-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspanspan-iddisplayingprocessesandthreadsspansection-9-displaying-processes-and-threads"></a><span id="DisplayingProcessesAndThreads"></span><span id="displayingprocessesandthreads"></span><span id="DISPLAYINGPROCESSESANDTHREADS"></span>第9部分：显示进程和线程

### <a name="span-idprocessesspanspan-idprocessesspanspan-idprocessesspanprocesses"></a><span id="Processes"></span><span id="processes"></span><span id="PROCESSES"></span>工艺

*在第9部分中，将显示有关在内核模式下运行的进程和线程的信息。*

**注意**  
您可以使用[**！ process**](-process.md)调试器扩展显示或设置过程信息。 我们将设置一个断点来检查播放声音时使用的进程。



1. **&lt;-在主机系统上**

   键入**dv**命令来检查与**EchoEvtIo**例程关联的区域设置变量，如下所示。

   ```dbgcmd
   0: kd> dv ECHO!EchoEvtIo*
   ECHO!EchoEvtIoQueueContextDestroy
   ECHO!EchoEvtIoWrite
   ECHO!EchoEvtIoRead         
   ```

2. 使用**bc \* **清除以前的断点。

   ```dbgcmd
   0: kd> bc *  
   ```

3. 3. 使用以下命令在**EchoEvtIo**例程上设置符号断点。

   ```dbgcmd
   0: kd> bm ECHO!EchoEvtIo*
     2: aade5490          @!”ECHO!EchoEvtIoQueueContextDestroy”
     3: aade55d0          @!”ECHO!EchoEvtIoWrite”
     4: aade54c0          @!”ECHO!EchoEvtIoRead”
   ```

4. 列出断点以确认是否正确设置了断点。

   ```dbgcmd
   0: kd> bl
   1 e aabf0490 [c:\Samples\kmdf echo sample\c++\driver\autosync\queue.c @ 197]    0001 (0001) ECHO!EchoEvtIoQueueContextDestroy
   ...
   ```

5. 键入**g**以重新启动代码执行。

   ```dbgcmd
   0: kd> g
   ```

6. **-&gt;在目标系统上**

   在目标系统上运行 EchoApp.exe 驱动程序测试程序。

7. **&lt;-在主机系统上**

   测试应用运行时，将调用驱动程序中的 i/o 例程。 这将导致触发断点，并使目标系统上的驱动程序代码执行停止。

   ```dbgcmd
   Breakpoint 2 hit
   ECHO!EchoEvtIoWrite:
   fffff801`0bf95810 4c89442418      mov     qword ptr [rsp+18h],r8
   ```

8. 使用 **！ process**命令显示运行 echoapp.exe 涉及的当前进程。

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

   此输出显示该进程与在命中驱动程序写入事件上的断点时正在运行的 echoapp.exe 相关联。 有关详细信息，请参阅[**！ process**](-process.md)。

9. 使用 **！ process 0 0**显示所有进程的摘要信息。 在输出中，使用 CTRL + F 定位与 echoapp.exe 映像关联的进程的相同进程地址。 在下面所示的示例中，进程地址为 ffffe0007e6a7780。

   ```dbgcmd
   ...

   PROCESS ffffe0007e6a7780
       SessionId: 1  Cid: 0f68    Peb: 7ff7cfe7a000  ParentCid: 0f34
       DirBase: 1f7fb9000  ObjectTable: ffffc001cec82780  HandleCount:  34.
       Image: echoapp.exe

   ...
   ```

10. 记录与 echoapp.exe 关联的进程 ID 以在此实验室稍后使用。 你还可以使用 CTRL + C 将地址复制到复制缓冲区以供以后使用。

    \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_（echoapp.exe 进程地址）

11. 在调试器中将**g**输入为必需，以便向前运行代码，直到 echoapp.exe 结束运行。 它会多次命中读写事件中的断点。 当 echoapp.exe 完成时，按 CTRL + ScrLk （Ctrl + Break）来中断调试器。

12. 使用 **！ process**命令确认现在正在运行不同的进程。 在下面显示的输出中，具有*系统*映像值的进程不同于*Echo* Image 值。

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

    上面的输出显示系统进程 ffffe0007b65d900 在停止操作系统时运行。

13. 现在，使用 **！ process**命令尝试查看与之前记录的 echoapp.exe 关联的进程 ID。 提供之前记录的 echoapp.exe 进程地址，而不是如下所示的示例过程地址。

    ```dbgcmd
    0: kd> !process ffffe0007e6a7780
    TYPE mismatch for process object at 82a9acc0
    ```

    由于 echoapp.exe 进程不再运行，因此进程对象不再可用。

### <a name="span-idthreadsspanspan-idthreadsspanspan-idthreadsspanthreads"></a><span id="Threads"></span><span id="threads"></span><span id="THREADS"></span>线程

**注意**  
用于查看和设置线程的命令与进程的命令非常相似。 使用[**！ thread**](-thread.md)命令查看线程。 使用[**. thread**](-thread--set-register-context-.md)设置当前线程。



1.  **&lt;-在主机系统上**

    将**g**输入到调试器中，以在目标系统上重新启动代码执行。

2.  **-&gt;在目标系统上**

    在目标系统上运行 EchoApp.exe 驱动程序测试程序。

3.  **&lt;-在主机系统上**

    断点将被命中，代码执行将暂停。

    ```dbgcmd
    Breakpoint 4 hit
    ECHO!EchoEvtIoRead:
    aade54c0 55              push    ebp
    ```

4.  若要查看正在运行的线程，请键入[**！ thread**](-thread.md)。 应显示类似于以下内容的信息：

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

    记下*echoapp.exe*的图像名称，这表示我们正在查看与测试应用程序关联的线程。

5.  4. 使用 **！ process**命令确定这是否是在与 echoapp.exe 关联的进程中运行的唯一线程。 请注意，进程中正在运行的线程的线程号就是运行的、！ thread 命令所运行的线程数。

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

6.  使用 **！ process 0 0 命令**查找两个相关进程的进程地址并在此处记录这些进程地址。

    Cmd.exe：\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp.exe：\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

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

    **注意** 您也可以使用 **！ process 0 17**来显示有关每个进程的详细信息。 此命令的输出可能很长。 可以使用 Ctrl + F 搜索输出。



7.  使用 **！ process**命令列出运行 PC 的两个进程的进程信息。 提供来自 **！ process 0 0**输出的进程地址，而不是如下所示的地址。

    此示例输出适用于先前记录的 cmd.exe 进程 ID。 请注意，此进程 ID 的映像名称是 cmd.exe。

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

    此示例输出适用于先前记录的 echoapp.exe 进程 ID。

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

8.  记录此处与这两个进程关联的第一个线程地址。

    Cmd.exe：\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

    EchoApp.exe：\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

9.  使用 **！** 用于显示有关当前线程的信息的线程命令。

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

    与预期一样，当前线程是与 echoapp.exe 相关联的线程，并且它处于运行状态。

10. 使用 **！** 用于显示与 cmd.exe 进程关联的线程相关信息的线程命令。 提供前面记录的线程地址。

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

    此线程与 cmd.exe 相关联，并且处于等待状态。

11. 提供等待线程的线程地址以将上下文更改为该等待线程的 CMD.exe 线程。

    ```dbgcmd
    0: kd> .Thread ffffe0007cf34880
    Implicit thread is now ffffe000`7cf34880
    ```

12. 使用**k**命令查看与等待线程关联的调用堆栈。

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

    调用 stack 元素（例如**KiCommitThreadWait** ）指示此线程未按预期运行。

**注意**  
有关线程和进程的详细信息，请参阅以下参考资料：

[线程和进程](threads-and-processes.md)

[更改上下文](changing-contexts.md)



## <a name="span-idsection_10__irql__registers_and_ending_the_windbg_sessionspanspan-idsection_10__irql__registers_and_ending_the_windbg_sessionspanspan-idsection_10__irql__registers_and_ending_the_windbg_sessionspansection-10-irql-registers-and-ending-the-windbg-session"></a><span id="Section_10__IRQL__Registers_and_Ending_the_WinDbg_session"></span><span id="section_10__irql__registers_and_ending_the_windbg_session"></span><span id="SECTION_10__IRQL__REGISTERS_AND_ENDING_THE_WINDBG_SESSION"></span>第10部分： IRQL、注册和结束 WinDbg 会话

### <a name="span-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanspan-idirqlregistersmemoryspanviewing-the-saved-irql"></a><span id="IRQLRegistersMemory"></span><span id="irqlregistersmemory"></span><span id="IRQLREGISTERSMEMORY"></span>查看保存的 IRQL

*在第10节中，您将显示 regsisters 的 IRQL 和内容。*

**&lt;-在主机系统上**

中断请求级别（IRQL）用于管理中断服务的优先级。 每个处理器都有一个可以提高或降低线程的 IRQL 设置。 在处理器的 IRQL 设置下或之下发生的中断会被屏蔽，并且不会影响当前操作。 超出处理器的 IRQL 设置的中断优先于当前操作。 在调试程序发生中断之前， [**！ irql**](-irql.md)扩展会在目标计算机的当前处理器上显示中断请求级别（irql）。 当目标计算机中断到调试器时，IRQL 会发生更改，但在调试器中断之前有效的 IRQL 会被保存，并由 **！ IRQL**显示。

```dbgcmd
0: kd> !irql
Debugger saved IRQL for processor 0x0 -- 2 (DISPATCH_LEVEL)
```

### <a name="span-idviewingtheregistersspanspan-idviewingtheregistersspanspan-idviewingtheregistersspanviewing-the-registers"></a><span id="ViewingTheRegisters"></span><span id="viewingtheregisters"></span><span id="VIEWINGTHEREGISTERS"></span>查看寄存器

**&lt;-在主机系统上**

使用[**r （寄存器）**](r--registers-.md)命令显示当前处理器上的当前线程的寄存器内容。

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

或者，您可以通过单击 "**查看**寄存器" 来显示寄存器内容 &gt; **registers**。 有关详细信息，请参阅[**r （寄存器）**](r--registers-.md)。

在单步执行汇编语言代码执行和其他情况时，查看寄存器的内容会很有帮助。 有关汇编语言反汇编的详细信息，请参阅[带批注的 X86 反汇编](annotated-x86-disassembly.md)和[带批注的 x64 反汇编](annotated-x64-disassembly.md)。

有关寄存器内容的信息，请参阅[X86 体系结构](x86-architecture.md)和[x64 体系结构](x64-architecture.md)。

### <a name="span-idendingthesessionspanspan-idendingthesessionspanspan-idendingthesessionspanending-the-windbg-session"></a><span id="EndingTheSession"></span><span id="endingthesession"></span><span id="ENDINGTHESESSION"></span>结束 WinDbg 会话

**&lt;-在主机系统上**

若要结束用户模式调试会话，请将调试器返回到休眠模式，然后将目标应用程序设置为再次运行，请输入**qd** （Quit 并分离）命令。

请确保并使用**g**命令让目标计算机运行代码，使其可以使用。 使用**bc \* **清除任何中断点也是一个不错的主意，这样一来，目标计算机将不会中断，而会尝试连接到主机计算机调试器。

```dbgcmd
0: kd> qd
```

有关详细信息，请参阅调试参考文档[中的在 WinDbg 结束调试会话](ending-a-debugging-session-in-windbg.md)。

## <a name="span-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspanspan-idwindowsdebuggingresourcesspansection-11-windows-debugging-resources"></a><span id="WindowsDebuggingResources"></span><span id="windowsdebuggingresources"></span><span id="WINDOWSDEBUGGINGRESOURCES"></span>第11节： Windows 调试资源


有关其他信息，请访问 Windows 调试。 请注意，其中的一些书籍将使用旧版 Windows （如 Windows Vista）的示例，但讨论的概念适用于大多数 Windows 版本。

**书籍**

-   Mario Hewardt 和 Daniel Pravat 的高级 Windows 调试

-   在 Windows 调试中：通过 Tarik Soulami 在 Windows®中调试和跟踪策略的实用指南

-   Windows 内部机制，Russinovich，David 为所罗门群岛和 Alex Ionescu

**视频**

碎片整理工具显示 WinDbg 剧集13-29<https://channel9.msdn.com/Shows/Defrag-Tools>

**培训供应商：**

OSR<https://www.osr.com/>

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[标准调试方法](standard-debugging-techniques.md)

[专业调试方法](specialized-debugging-techniques.md)

[Windows 调试入门](getting-started-with-windows-debugging.md)










