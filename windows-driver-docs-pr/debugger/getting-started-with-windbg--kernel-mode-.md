---
title: WinDbg 入门（内核模式）
description: 本主题提供的动手练习将帮助你开始使用 WinDbg 作为内核模式调试器。
ms.assetid: 1B61591F-0D48-4FBD-B242-68BB90D27FAF
ms.date: 02/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: f87672476bca81ec688877dd90e35d84092ad732
ms.sourcegitcommit: d03c24342b9852013301a37e2ec95592804204f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "77528975"
---
# <a name="span-iddebuggergetting_started_with_windbg__kernel-mode_spangetting-started-with-windbg-kernel-mode"></a><span id="debugger.getting_started_with_windbg__kernel-mode_"></span>与 WinDbg 入门（内核模式）

WinDbg 是 Windows 调试工具中包含的内核模式和用户模式调试器。 在这里，我们将提供实践练习，帮助你开始使用 WinDbg 作为内核模式调试器。

有关如何获取 Windows 调试工具的信息，请参阅[适用于 windows 的调试工具（WinDbg、KD、CDB、NTSD）](index.md)。 安装调试工具后，找到64位（x64）和32位（x86）版本的工具的安装目录。 例如：

- C：\\Program Files （x86）\\Windows 工具包\\10\\调试器\\x64
- C：\\Program Files （x86）\\Windows 工具包\\10\\调试器\\x86

## <a name="span-idset_up_a_kernel-mode_debuggingspanspan-idset_up_a_kernel-mode_debuggingspanspan-idset_up_a_kernel-mode_debuggingspanset-up-a-kernel-mode-debugging"></a><span id="Set_up_a_kernel-mode_debugging"></span><span id="set_up_a_kernel-mode_debugging"></span><span id="SET_UP_A_KERNEL-MODE_DEBUGGING"></span>设置内核模式调试

内核模式调试环境通常具有两台计算机：*主计算机*和*目标计算机*。 调试器在主计算机上运行，要调试的代码在目标计算机上运行。 主机和目标由调试电缆进行连接。

Windows 调试器支持以下类型的缆线用于调试：

- 以太网
- USB 2.0/USB 3。0
- 串行（也称为空调制解调器）

为实现速度和可靠性，建议结合使用以太网和本地网络中心。 此图说明了已连接以便通过以太网电缆进行调试的主机和目标计算机。

![通过以太网连接的主机和目标示意图](images/configfortest01.png)

Windows 的较早版本的另一个选项是使用 USB 或串行电缆等直接电缆。 

![带有调试电缆的主机和目标示意图](images/configfortest02.png)

有关如何设置主机和目标计算机的详细信息，请参阅[手动设置内核模式调试](setting-up-kernel-mode-debugging-in-windbg--cdb--or-ntsd.md)。

### <a name="virtual-machine---vms"></a>虚拟机-Vm

有关将调试程序连接到 Hyper-v 虚拟机的信息，请参阅[设置虚拟机的网络调试-KDNET](setting-up-network-debugging-of-a-virtual-machine-host.md)。

## <a name="span-idestablish_a_kernel-mode_debugging_sessionspanspan-idestablish_a_kernel-mode_debugging_sessionspanspan-idestablish_a_kernel-mode_debugging_sessionspanestablish-a-kernel-mode-debugging-session"></a><span id="Establish_a_kernel-mode_debugging_session"></span><span id="establish_a_kernel-mode_debugging_session"></span><span id="ESTABLISH_A_KERNEL-MODE_DEBUGGING_SESSION"></span>建立内核模式调试会话


设置好主机和目标计算机并将其与调试电缆连接后，可以按照用于设置的同一主题中的说明建立内核模式调试会话。 例如，如果决定将主机和目标计算机设置为通过以太网进行调试，则可以在本主题中找到有关建立内核模式调试会话的说明：

-  [自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)


## <a name="span-idget_started_using_windbgspanspan-idget_started_using_windbgspanspan-idget_started_using_windbgspanget-started-using-windbg"></a><span id="Get_started_using_WinDbg"></span><span id="get_started_using_windbg"></span><span id="GET_STARTED_USING_WINDBG"></span>使用 WinDbg 开始使用


1. 在主计算机上，打开 WinDbg 并建立与目标计算机的内核模式调试会话。
2. 在 WinDbg 的 "**帮助**" 菜单中选择 "**内容**"。 这会打开调试器文档 CHM 文件。 [此处](index.md)还提供了调试器文档。
3. 建立内核模式调试会话时，WinDbg 可能会自动中断目标计算机。 如果 WinDbg 尚未在中出现，请从 "**调试**" 菜单中选择 "**中断**"。

4. 在 "WinDbg" 窗口底部附近的命令行中，输入以下命令：

   [ **。 sympath srv\\** *](https://go.microsoft.com/fwlink/p?linkid=399238)

   输出类似于以下内容：

   ```dbgcmd
   Symbol search path is: srv*
   Expanded Symbol search path is: cache*;SRV*https://msdl.microsoft.com/download/symbols
   ```

   符号搜索路径指示 WinDbg 查找符号（PDB）文件的位置。 调试器需要符号文件来获取有关代码模块的信息（函数名、变量名和 like）。

   输入此命令，该命令会告诉 WinDbg 完成符号文件的初始查找和加载：

   [ **。重装**](https://go.microsoft.com/fwlink/p?linkid=399239)

5. 若要查看已加载的模块的列表，请输入以下命令：

   [**lm**](https://go.microsoft.com/fwlink/p?linkid=399237)

   输出类似于以下内容：

   ```dbgcmd
   0:000>3: kd> lm
   start             end                 module name
   fffff800`00000000 fffff800`00088000   CI         (deferred)             
   ...         
   fffff800`01143000 fffff800`01151000   BasicRender   (deferred)             
   fffff800`01151000 fffff800`01163000   BasicDisplay  (deferred)             
   ...      
   fffff800`02a0e000 fffff800`03191000   nt  (pdb symbols) C:\...\ntkrnlmp.pdb
   fffff800`03191000 fffff800`03200000   hal (deferred)             
   ...
   ```

6. 若要启动运行的目标计算机，请输入以下命令：

   [**g**](https://go.microsoft.com/fwlink/p?linkid=399388)

7. 若要再次中断，请选择 "**调试**" 菜单中的 "**中断**"。

8. 输入以下命令以检查 nt 模块中 \_文件\_对象数据类型：

   [**dt nt！\_文件\_对象**](https://go.microsoft.com/fwlink/p?linkid=399397)

   输出类似于以下内容：

   ```dbgcmd
   0:000>0: kd> dt nt!_FILE_OBJECT
      +0x000 Type             : Int2B
      +0x002 Size             : Int2B
      +0x008 DeviceObject     : Ptr64 _DEVICE_OBJECT
      +0x010 Vpb              : Ptr64 _VPB
      ...
      +0x0c0 IrpList          : _LIST_ENTRY
      +0x0d0 FileObjectExtension : Ptr64 Void
   ```

9. 输入以下命令以检查 nt 模块中的某些符号：

   [**x nt！\\\*CreateProcess***](https://go.microsoft.com/fwlink/p?linkid=399240)

   输出类似于以下内容：

   ```dbgcmd
   0:000>0: kd> x nt!*CreateProcess*
   fffff800`030821cc nt!ViCreateProcessCallbackInternal (<no parameter info>)
   ...
   fffff800`02e03904 nt!MmCreateProcessAddressSpace (<no parameter info>)
   fffff800`02cece00 nt!PspCreateProcessNotifyRoutine = <no type information>
   ...
   ```

10. 输入以下命令，在**MmCreateProcessAddressSpace**放置断点：

    [**bu nt！MmCreateProcessAddressSpace**](https://go.microsoft.com/fwlink/p?linkid=399390)

    若要验证是否已设置断点，请输入以下命令：

    [**bl**](https://go.microsoft.com/fwlink/p?linkid=399391)

    输出类似于以下内容：

    ```dbgcmd
    0:000>0: kd> bu nt!MmCreateProcessAddressSpace
    0: kd> bl
    0 e fffff800`02e03904     0001 (0001) nt!MmCreateProcessAddressSpace
    ```

    输入[**g**](https://go.microsoft.com/fwlink/p?linkid=399388)允许目标计算机运行。

11. 如果目标计算机不立即进入调试器，请在目标计算机上执行几项操作（例如，打开记事本）。 调用**MmCreateProcessAddressSpace**时，目标计算机将中断到调试器。 若要查看堆栈跟踪，请输入以下命令：

    [ **。重装**](https://go.microsoft.com/fwlink/p?linkid=399239)

    [**温度**](https://go.microsoft.com/fwlink/p?linkid=399389)

    输出类似于以下内容：

    ```dbgcmd
    0:000>2: kd> k
    Child-SP          RetAddr           Call Site
    ffffd000`224b4c88 fffff800`02d96834 nt!MmCreateProcessAddressSpace
    ffffd000`224b4c90 fffff800`02dfef17 nt!PspAllocateProcess+0x5d4
    ffffd000`224b5060 fffff800`02b698b3 nt!NtCreateUserProcess+0x55b
    ...
    000000d7`4167fbb0 00007ffd`14b064ad KERNEL32!BaseThreadInitThunk+0xd
    000000d7`4167fbe0 00000000`00000000 ntdll!RtlUserThreadStart+0x1d
    ```

12. 在 "**视图**" 菜单上，选择 "**反汇编**"。

    在 "**调试**" 菜单上，选择 "**逐过程**" （或按**F10**）。 在观看 "反汇编" 窗口时，多次输入步骤命令。

13. 输入以下命令以清除断点：

    [**bc \\** *](https://go.microsoft.com/fwlink/p?linkid=399401)

    输入[**g**](https://go.microsoft.com/fwlink/p?linkid=399388)允许目标计算机运行。 通过选择 "**调试**" 菜单中的 "**中断**" 或按**CTRL break**再次中断。

14. 若要查看所有进程的列表，请输入以下命令：

    [ **！进程 0 0**](https://go.microsoft.com/fwlink/p?linkid=399241)

    输出类似于以下内容：

    ```dbgcmd
    0:000>0: kd> !process 0 0
    **** NT ACTIVE PROCESS DUMP ****
    PROCESS ffffe000002287c0
        SessionId: none  Cid: 0004    Peb: 00000000  ParentCid: 0000
        DirBase: 001aa000  ObjectTable: ffffc00000003000  HandleCount: <Data Not Accessible>
        Image: System

    PROCESS ffffe00001e5a900
        SessionId: none  Cid: 0124    Peb: 7ff7809df000  ParentCid: 0004
        DirBase: 100595000  ObjectTable: ffffc000002c5680  HandleCount: <Data Not Accessible>
        Image: smss.exe
    ...
    PROCESS ffffe00000d52900
        SessionId: 1  Cid: 0910    Peb: 7ff669b8e000  ParentCid: 0a98
        DirBase: 3fdba000  ObjectTable: ffffc00007bfd540  HandleCount: <Data Not Accessible>
        Image: explorer.exe
    ```

15. 复制一个进程的地址，然后输入以下命令：

    [ **！进程***地址* **2**](https://go.microsoft.com/fwlink/p?linkid=399241)

    例如： **！ process ffffe00000d5290 2**

    输出显示进程中的线程。

    ```dbgcmd
    0:000>0:000>0: kd> !process ffffe00000d52900 2
    PROCESS ffffe00000d52900
        SessionId: 1  Cid: 0910    Peb: 7ff669b8e000  ParentCid: 0a98
        DirBase: 3fdba000  ObjectTable: ffffc00007bfd540  HandleCount:
        Image: explorer.exe

            THREAD ffffe00000a0d880  Cid 0910.090c  Teb: 00007ff669b8c000
                ffffe00000d57700  SynchronizationEvent

            THREAD ffffe00000e48880  Cid 0910.0ad8  Teb: 00007ff669b8a000
                ffffe00000d8e230  NotificationEvent
                ffffe00000cf6870  Semaphore Limit 0xffff
                ffffe000039c48c0  SynchronizationEvent
            ...
            THREAD ffffe00000e6d080  Cid 0910.0cc0  Teb: 00007ff669a10000
                ffffe0000089a300  QueueObject
    ```

16. 复制一个线程的地址，然后输入以下命令：

    [ **！线程***地址*](https://go.microsoft.com/fwlink/p?linkid=399244)

    例如： **！ thread ffffe00000e6d080**

    输出显示有关各个线程的信息。

    ```dbgcmd
    0: kd> !thread ffffe00000e6d080
    THREAD ffffe00000e6d080  Cid 0910.0cc0  Teb: 00007ff669a10000 Win32Thread: 0000000000000000 WAIT: ...
        ffffe0000089a300  QueueObject
    Not impersonating
    DeviceMap                 ffffc000034e7840
    Owning Process            ffffe00000d52900       Image:         explorer.exe
    Attached Process          N/A            Image:         N/A
    Wait Start TickCount      13777          Ticks: 2 (0:00:00:00.031)
    Context Switch Count      2              IdealProcessor: 1             
    UserTime                  00:00:00.000
    KernelTime                00:00:00.000
    Win32 Start Address ntdll!TppWorkerThread (0x00007ffd14ab2850)
    Stack Init ffffd00021bf1dd0 Current ffffd00021bf1580
    Base ffffd00021bf2000 Limit ffffd00021bec000 Call 0
    Priority 13 BasePriority 13 UnusualBoost 0 ForegroundBoost 0 IoPriority 2 PagePriority 5
    ...
    ```

17. 若要查看即插即用设备树中的所有设备节点，请输入以下命令：

    [ **！ devnode 0 1**](https://go.microsoft.com/fwlink/p?linkid=399242)

    ```dbgcmd
    0:000>0: kd> !devnode 0 1
    Dumping IopRootDeviceNode (= 0xffffe000002dbd30)
    DevNode 0xffffe000002dbd30 for PDO 0xffffe000002dc9e0
      InstancePath is "HTREE\ROOT\0"
      State = DeviceNodeStarted (0x308)
      Previous State = DeviceNodeEnumerateCompletion (0x30d)
      DevNode 0xffffe000002d9d30 for PDO 0xffffe000002daa40
        InstancePath is "ROOT\volmgr\0000"
        ServiceName is "volmgr"
        State = DeviceNodeStarted (0x308)
        Previous State = DeviceNodeEnumerateCompletion (0x30d)
        DevNode 0xffffe00001d49290 for PDO 0xffffe000002a9a90
          InstancePath is "STORAGE\Volume\{3007dfd3-df8d-11e3-824c-806e6f6e6963}#0000000000100000"
          ServiceName is "volsnap"
          TargetDeviceNotify List - f 0xffffc0000031b520  b 0xffffc0000008d0f0
          State = DeviceNodeStarted (0x308)
          Previous State = DeviceNodeStartPostWork (0x307)
    ...
    ```

18. 若要查看设备节点及其硬件资源，请输入以下命令：

    [ **！ devnode 0 9**](https://go.microsoft.com/fwlink/p?linkid=399242)

    ```dbgcmd
    0:000>...
            DevNode 0xffffe000010fa770 for PDO 0xffffe000010c2060
              InstancePath is "PCI\VEN_8086&DEV_2937&SUBSYS_2819103C&REV_02\3&33fd14ca&0&D0"
              ServiceName is "usbuhci"
              State = DeviceNodeStarted (0x308)
              Previous State = DeviceNodeEnumerateCompletion (0x30d)
              TranslatedResourceList at 0xffffc00003c78b00  Version 1.1  Interface 0x5  Bus #0
                Entry 0 - Port (0x1) Device Exclusive (0x1)
                  Flags (0x131) - PORT_MEMORY PORT_IO 16_BIT_DECODE POSITIVE_DECODE 
                  Range starts at 0x3120 for 0x20 bytes
                Entry 1 - DevicePrivate (0x81) Device Exclusive (0x1)
                  Flags (0000) - 
                  Data - {0x00000001, 0x00000004, 0000000000}
                Entry 2 - Interrupt (0x2) Shared (0x3)
                  Flags (0000) - LEVEL_SENSITIVE 
                  Level 0x8, Vector 0x81, Group 0, Affinity 0xf
    ...
    ```

19. 若要查看具有磁盘服务名称的设备节点，请输入以下命令：

    [ **！ devnode 0 1 磁盘**](https://go.microsoft.com/fwlink/p?linkid=399242)

    ```dbgcmd
    0: kd> !devnode 0 1 disk
    Dumping IopRootDeviceNode (= 0xffffe000002dbd30)
    DevNode 0xffffe0000114fd30 for PDO 0xffffe00001159610
      InstancePath is "IDE\DiskST3250820AS_____________________________3.CHL___\5&14544e82&0&0.0.0"
      ServiceName is "disk"
      State = DeviceNodeStarted (0x308)
      Previous State = DeviceNodeEnumerateCompletion (0x30d)
    ...
    ```

20. [ **！ Devnode 0 1**](https://go.microsoft.com/fwlink/p?linkid=399242)的输出显示节点的物理设备对象（PDO）的地址。 复制物理设备对象（PDO）的地址，然后输入以下命令：

    [ **！ devstack** *PdoAddress*](https://go.microsoft.com/fwlink/p?linkid=399245)

    例如： <em>PdoAddress</em> **！ devstack 0xffffe00001159610**

    ```dbgcmd
    0:000>0: kd> !devstack 0xffffe00001159610
      !DevObj           !DrvObj            !DevExt           ObjectName
      ffffe00001d50040  \Driver\partmgr    ffffe00001d50190  
      ffffe00001d51450  \Driver\disk       ffffe00001d515a0  DR0
      ffffe00001156e50  \Driver\ACPI       ffffe000010d8bf0  
    ```

21. 若要获取有关驱动程序 disk .sys 的信息，请输入以下命令：

    [ **！ drvobj disk 2**](https://go.microsoft.com/fwlink/p?linkid=399246)

    ```dbgcmd
    0:000>0: kd> !drvobj disk 2
    Driver object (ffffe00001d52680) is for:
     \Driver\disk
    DriverEntry:   fffff800006b1270 disk!GsDriverEntry
    DriverStartIo: 00000000 
    DriverUnload:  fffff800010b0b5c CLASSPNP!ClassUnload
    AddDevice:     fffff800010aa110 CLASSPNP!ClassAddDevice

    Dispatch routines:
    [00] IRP_MJ_CREATE                      fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    [01] IRP_MJ_CREATE_NAMED_PIPE           fffff80002b0ab24    nt!IopInvalidDeviceRequest
    [02] IRP_MJ_CLOSE                       fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    [03] IRP_MJ_READ                        fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    ...
    [1b] IRP_MJ_PNP                         fffff8000106d160    CLASSPNP!ClassGlobalDispatch
    ```

22. ！ Drvobj 的输出显示调度例程的地址：例如，CLASSPNP！ClassGlobalDispatch. 若要在 ClassGlobalDispatch 上设置和验证断点，请输入以下命令：

    [**bu CLASSPNP！ClassGlobalDispatch**](https://go.microsoft.com/fwlink/p?linkid=399390)

    [**bl**](https://go.microsoft.com/fwlink/p?linkid=399391)

    输入 g 允许目标计算机运行。

    如果目标计算机不立即进入调试器，请在目标计算机上执行几项操作（例如，打开记事本并保存文件）。 调用**ClassGlobalDispatch**时，目标计算机将中断到调试器。 若要查看堆栈跟踪，请输入以下命令：

    [ **。重装**](https://go.microsoft.com/fwlink/p?linkid=399239)

    [**温度**](https://go.microsoft.com/fwlink/p?linkid=399389)

    输出类似于以下内容：

    ```dbgcmd
    2: kd> k
    Child-SP          RetAddr           Call Site
    ffffd000`21d06cf8 fffff800`0056c14e CLASSPNP!ClassGlobalDispatch
    ffffd000`21d06d00 fffff800`00f2c31d volmgr!VmReadWrite+0x13e
    ffffd000`21d06d40 fffff800`0064515d fvevol!FveFilterRundownReadWrite+0x28d
    ffffd000`21d06e20 fffff800`0064578b rdyboost!SmdProcessReadWrite+0x14d
    ffffd000`21d06ef0 fffff800`00fb06ad rdyboost!SmdDispatchReadWrite+0x8b
    ffffd000`21d06f20 fffff800`0085cef5 volsnap!VolSnapReadFilter+0x5d
    ffffd000`21d06f50 fffff800`02b619f7 Ntfs!NtfsStorageDriverCallout+0x16
    ...
    ```

23. 若要结束调试会话，请输入以下命令：

    [**qd**](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idsummary_of_commandsspanspan-idsummary_of_commandsspanspan-idsummary_of_commandsspansummary-of-commands"></a><span id="Summary_of_commands"></span><span id="summary_of_commands"></span><span id="SUMMARY_OF_COMMANDS"></span>命令摘要


-   "**帮助**" 菜单上的 "**内容**" 命令
-   [. sympath （设置符号路径）](https://go.microsoft.com/fwlink/p?linkid=399238)
-   [。重载（重载模块）](https://go.microsoft.com/fwlink/p?linkid=399239)
-   [x （检查符号）](https://go.microsoft.com/fwlink/p?linkid=399240)
-   [g （走）](https://go.microsoft.com/fwlink/p?linkid=399388)
-   [dt （显示类型）](https://go.microsoft.com/fwlink/p?linkid=399397)
-   "**调试**" 菜单上的 "**中断**" 命令
-   [lm （列出加载的模块）](https://go.microsoft.com/fwlink/p?linkid=399237)
-   [k （显示 Stack Backtrace）](https://go.microsoft.com/fwlink/p?linkid=399389)
-   [bu （设置断点）](https://go.microsoft.com/fwlink/p?linkid=399390)
-   [bl （断点列表）](https://go.microsoft.com/fwlink/p?linkid=399391)
-   [bc （中断清除）](https://go.microsoft.com/fwlink/p?linkid=399401)
-   "**调试**" 菜单上的 "**单步**执行" 命令（**F11**）
-   [！进程](https://go.microsoft.com/fwlink/p?linkid=399241)
-   [！ thread](https://go.microsoft.com/fwlink/p?linkid=399244)
-   [!devnode](https://go.microsoft.com/fwlink/p?linkid=399242)
-   [!devstack](https://go.microsoft.com/fwlink/p?linkid=399245)
-   [!drvobj](https://go.microsoft.com/fwlink/p?linkid=399246)
-   [qd （退出并分离）](https://go.microsoft.com/fwlink/p?linkid=399394)

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[Getting Started with WinDbg (User-Mode)](getting-started-with-windbg.md)（WinDbg 入门（用户模式））

[自动设置 KDNET 网络内核调试](setting-up-a-network-debugging-connection-automatically.md)

[调试程序操作](debugger-operation-win8.md)

[调试方法](debugging-techniques.md)

[适用于 Windows 的调试工具（WinDbg、KD、CDB、NTSD）](https://docs.microsoft.com/windows-hardware/drivers/debugger/)

[使用 WinDbg Preview 进行调试](debugging-using-windbg-preview.md)