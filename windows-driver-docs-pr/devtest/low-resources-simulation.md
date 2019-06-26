---
title: 资源不足模拟
description: 资源不足模拟
ms.assetid: 2710fa23-26cd-493b-abb4-3a0969a98eb1
keywords:
- 低资源模拟选项 WDK Driver Verifier
- 内存不足的检查 WDK Driver Verifier
- 内存不足，无法检查 WDK Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1f5391d090d5cfa1a1a665e1df34fb914623b0f7
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354779"
---
# <a name="low-resources-simulation"></a>资源不足模拟


## <span id="ddk_low_resources_simulation_tools"></span><span id="DDK_LOW_RESOURCES_SIMULATION_TOOLS"></span>


当低资源模拟选项 (名为*随机化的资源不足模拟*Windows 8.1 中) 是处于活动状态，驱动程序验证程序进行故障的驱动程序的内存分配随机实例，如果该驱动程序上运行可能会出现内存不足的计算机。 这会测试驱动程序的正确响应内存不足和其他资源不足的情况的能力。

低资源模拟测试失败请求的多个不同的功能，包括对的调用的分配[ **ExAllocatePoolWithXXX**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)， [ **MmGetSystemAddressForMdlSafe**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)， [ **MmProbeAndLockPages**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmprobeandlockpages)， [ **MmMapLockedPagesSpecifyCache** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmaplockedpagesspecifycache)，并[ **MmMapIoSpace**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmmapiospace)。

从 Windows Vista 开始，低资源模拟测试还会注入到的错误[ **IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)， [ **IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)，[ **IoAllocateWorkItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateworkitem)， [ **IoAllocateErrorLogEntry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateerrorlogentry)， [ **MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemory)， [ **MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)， [ **MmAllocatePagesForMdl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdl)，并[ **MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)。 此外，Windows vista 中，从开始，启用低资源模拟时，调用[ **KeWaitForMultipleObjects** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitformultipleobjects)或[ **KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kewaitforsingleobject)与*Alertable*参数设置为**TRUE**可以返回状态\_低权限的进程的上下文中运行时向你发出警报。 这模拟的是来自同一非特权应用程序中的另一个线程可能线程警报。

低资源模拟测试还将故障注入到以下的 GDI 函数：[**EngAllocMem**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocmem)， [ **EngAllocUserMem**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engallocusermem)， [ **EngCreateBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatebitmap)， [ **EngCreateDeviceSurface**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicesurface)， [ **EngCreateDeviceBitmap**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedevicebitmap)， [ **EngCreatePalette** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepalette)， [ **EngCreateClip**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreateclip)， [ **EngCreatePath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatepath)， [ **EngCreateWnd**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatewnd)， [ **EngCreateDriverObj**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatedriverobj)， [ **BRUSHOBJ\_pvAllocRbrush**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-brushobj_pvallocrbrush)，和[**CLIPOBJ\_ppoGetPath**](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-clipobj_ppogetpath)。

在 Windows 7 和更高版本的 Windows 操作系统中，低资源模拟选项支持使用以下内核 Api 分配的内存：

-   [**IoAllocateMdl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocatemdl)

-   [**IoAllocateIrp** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioallocateirp)和其他例程可以分配 I/O 请求数据包 (IRP) 数据结构

-   [**RtlAnsiStringToUnicodeString** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlansistringtounicodestring)和其他运行时库 (RTL) 的字符串例程

-   [**IoSetCompletionRoutineEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetcompletionroutineex)

从 Windows 8.1 开始，低资源模拟选项也会失败分配请求的对 MmAllocateNodePagesForMdlEx 的调用。 此外，对于某些函数，驱动程序验证程序现在将填充具有随机模式已分配的内存。 但仅在函数为其返回未初始化的内存的情况下。 这些功能包括：

-   [**MmAllocatePagesForMdlEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatepagesformdlex)
-   MmAllocateNodePagesForMdlEx
-   [**MmAllocateContiguousMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemory)
-   [**MmAllocateContiguousMemorySpecifyCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)
-   [**MmAllocateContiguousMemorySpecifyCacheNode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycachenode)
-   [**MmAllocateContiguousNodeMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-mmallocatecontiguousnodememory)
-   [**MmAllocateNonCachedMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-mmallocatenoncachedmemory)

### <a name="span-idcustomsettingsforlowresourcessimulationspanspan-idcustomsettingsforlowresourcessimulationspancustom-settings-for-low-resources-simulation"></a><span id="custom_settings_for_low_resources_simulation"></span><span id="CUSTOM_SETTINGS_FOR_LOW_RESOURCES_SIMULATION"></span>资源不足模拟的自定义设置

在 Windows Vista 和更高版本的 Windows 中，可以指定以下自定义设置。

-   **概率**，给定的分配会失败。 默认值为 6%。

-   **应用程序**受影响。 此设置限制了插入失败，分配到指定的应用程序。 默认情况下，所有分配会受到都影响。

-   **池标记**受影响。 此设置将限制到分配，则使用指定的池标记的注入的错误。 默认情况下，所有分配会受到都影响。

-   **延迟**（以分钟为单位） 之前失败的分配。 此延迟可让系统启动和稳定后再注入错误。 默认值为八分钟。

在 Windows Vista 之前的操作系统，不能自定义这些设置。 操作系统使用的默认值。

### <a name="span-idlowresourcessimulationwithoutrebootingspanspan-idlowresourcessimulationwithoutrebootingspanlow-resources-simulation-without-rebooting"></a><span id="low_resources_simulation_without_rebooting"></span><span id="LOW_RESOURCES_SIMULATION_WITHOUT_REBOOTING"></span>资源不足而不必重新启动模拟

可以激活 Windows 2000 和更高版本的 Windows 上的低资源模拟，无需重新启动计算机，通过使用 **/volatile**参数。 设置将立即生效，但如果你关闭或重新启动计算机都将丢失。

您还可以将存储的低资源模拟设置注册表通过省略 **/volatile**参数。 仅当重新启动计算机，但它们保持有效，直到更改它们时，这些设置是有效的。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的低资源模拟选项。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

-   **在命令行**

    在命令行中，由表示低资源模拟选项**位 2 (0x4)** 。 若要激活低资源模拟，请使用 0x4 标志值或将 0x4 添加到标志值。 例如：

    ```
    verifier /flags 0x4 /driver MyDriver.sys
    ```

    在下一次启动后，选项将处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，可以使用 */错误*参数或标志值**0x4**激活低资源模拟。 若要修改的低资源模拟设置，必须使用 **/错误**。 例如：

    ```
    verifier /faults /driver MyDriver.sys
    ```

    在 Windows 2000 和更高版本的 Windows，您可以还激活和停低资源模拟用而无需重启计算机，通过添加 **/volatile**命令参数。 例如：

    ```
    verifier /volatile /flags 0x4 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

    在 Windows Vista 中，可以使用 **/错误**参数以表示与低资源模拟 **/volatile**参数以表示不重启是有效的设置。 将显示设置更改。 例如：

    ```
    0>  verifier /volatile /faults /adddriver MyDriver.sys
    New Low Resources Simulation options:

    - Use default fault injection probability.
    - Allocations using any pool tag can be failed.
    - Simulate low resources conditions in any application.

    The new settings are in effect until you restart this computer
    or change them again.
    ```

-   **使用驱动程序验证程序管理器**
    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择**较低的资源模拟**。

### <a name="span-idcustomizingthesettingswindowsvistaandlaterspanspan-idcustomizingthesettingswindowsvistaandlaterspancustomizing-the-settings-windows-vista-and-later"></a><span id="customizing_the_settings__windows_vista_and_later_"></span><span id="CUSTOMIZING_THE_SETTINGS__WINDOWS_VISTA_AND_LATER_"></span>自定义设置 (Windows Vista 及更高版本)

从 Windows Vista 开始，你可以延迟、 概率、 应用程序的默认设置和池标记低资源模拟选项的属性。 可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来更改这些设置。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

在命令行中，这些设置的语法如下所示：

**verifier** \[ **/volatile**\] **/faults**\[*Probability*|*PoolTags*|*Applications*|*DelayMins*\]\[ **/driver**|*DriverList*\]

**请注意**自定义设置参数必须出现在显示的顺序。 如果省略一个值，键入引号，若要保留它的位置。



**子参数**

- **/faults**

  使驱动程序验证程序中的低资源模拟选项。 （您不能使用 /flags 0x4 与自定义设置子参数。）

- *概率*

  指定驱动程序验证程序将失败的给定的分配的概率。 键入一个数字 （以十进制或十六进制格式） 的可能性将数量表示在驱动程序验证程序将失败分配 10,000。 默认值为 600，表示 600/10000 或 6%。

- *PoolTags*

  限制驱动程序验证程序可以分配，则使用指定的池标记为失败的分配。 可以使用通配符 (* *\\* * *) 来表示池的多个标记。 若要列出多个池标记，请用空格分隔标记。 默认情况下，所有分配可能会都失败。

- *Applications*

  限制驱动程序验证程序可以故障到指定的程序的分配的分配。 键入可执行文件的名称。 若要列出的程序，单独的程序名称以空格。 默认情况下，所有分配可能会都失败。

- *DelayMins*

  指定在此期间驱动程序验证程序不会有意失败任何分配的启动后的分钟数。 此延迟使用要加载的驱动程序和系统在测试前达到稳定状态开始。 键入一个数字 （以十进制或十六进制格式）。 默认值为 8 （分钟）。

例如，以下命令启用低资源模拟有 10%的可能性 (1000年/10000) 和池标记，标记 1 和 Fred，和应用程序，Notepad.exe 的五分钟的延迟。

```
verifier /faults 1000 "Tag1 Fred" Notepad.exe 5
```

以下命令可同时低资源模拟具有默认值，只不过它扩展到 10 分钟的延迟。

```
verifier /faults "" "" "" 0xa
```

**使用驱动程序验证程序管理器**

1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
2.  选择**创建自定义设置 （适用于代码开发人员）** ，然后单击**下一步**。

3.  选择**从完整的列表中选择单个设置**。

4.  选择**较低的资源模拟**，然后单击**下一步。**

5.  更改延迟、 概率、 应用程序的设置和池标记为所需的属性。

### <a name="span-idviewingtheresultsspanspan-idviewingtheresultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>查看结果

你可以监视的 Driver Verifier 有意失败的资源分配通过显示驱动程序验证程序的次数*注入错误*全局计数器。 此计数器显示自上次启动以来有意失败，驱动程序验证程序的资源分配的总数。

可以在驱动程序验证程序的日志文件查看此计数器 ( **/log**)，在命令行 ( **/查询**) 或驱动程序验证器管理器中。 在 Windows 2000 中，若要查看全局计数器，请选择**全局计数器**选项卡。在更高版本的 Windows 中，选择**显示有关当前已验证的驱动程序的信息**任务，，然后按**下一步**两次。 有关详细信息请参阅[监视全局计数器](monitoring-global-counters.md)。

您还可以通过使用显示有意失败的分配数和总分配 （若要计算的概率） 数 **！ verifier**调试器扩展。 下面的示例演示的示例 **！ verifier**输出。

在此示例中，**注入随机资源较少的 API 故障**指示低资源模拟已启用。 **资源分配有意失败**表示有意失败的分配数并**池的分配尝试**表示的总分配数。

```
!verifier

Verify Level 5 ... enabled options are:
        Special pool
        Inject random low-resource API failures

Summary of All Verifier Statistics

RaiseIrqls                             0x2c671f
AcquireSpinLocks                       0xca1a02
Synch Executions                       0x10a623
Trims                                  0x0

Pool Allocations Attempted             0x862e0e
Pool Allocations Succeeded             0x8626e3
Pool Allocations Succeeded SpecialPool 0x768060
Pool Allocations With NO TAG           0x0
Pool Allocations Failed                0x34f
Resource Allocations Failed Deliberately   0x3f5
```

若要显示最新驱动程序验证程序失败的分配堆栈跟踪，请使用 **！ verifier 4**内核调试器中。

下面的示例演示一个示例的输出 **！ verifier 4**。 默认情况下 **！ verifier 4**显示堆栈跟踪从四个最最近失败的分配，但你可以使用其*Quantity*参数以增加堆栈跟踪显示的数量。 例如，！ verifier 0x80 显示 128 最近失败的分配。

在此示例中，请注意验证工具已拦截和替换的驱动程序调用**ExAllocatePoolWithTag**。 驱动程序故障的最常见的原因之一发生时驱动程序将尝试分配内存，然后使用验证不之前返回的分配函数的指针**NULL**。

```
kd> !verifier 4
Resource fault injection history:
Tracker @ 8354A000 (# entries: 80, size: 80, depth: 8)

Entry @ 8354B258 (index 75)

    Thread: C2638220

    816760CB nt!VerifierExAllocatePoolWithTag+0x49
    A4720443 win32k!bDeleteAllFlEntry+0x15d
    A4720AB0 win32k!GreEnableEUDC+0x70
    A47218FA win32k!CleanUpEUDC+0x37
    A473998E win32k!GdiMultiUserFontCleanup+0x5
    815AEACC nt!MiDereferenceSession+0x74
    8146D3B4 nt!MmCleanProcessAddressSpace+0x112
    815DF739 nt!PspExitThread+0x603

Entry @ 8354B230 (index 74)

    Thread: 8436D770

    816760CB nt!VerifierExAllocatePoolWithTag+0x49
    A462141C win32k!Win32AllocPool+0x13
    A4725F94 win32k!StubGdiAlloc+0x10
```

与低资源模拟测试体验显示大多数驱动程序崩溃由最近失败的分配。 在上面的示例中，在发生崩溃时的路径中**win32k ！GreEnableEUDC**。 检查以找出在发生崩溃的原因的分配的路径中的代码。

璝惠 **！ verifier**，请参阅*的 Windows 调试工具*文档。

若要在注册表中的命令行中查看设置，请使用 **/querysettings**选项。 例如：

```
C:\>verifier /querysettings
Special pool: Disabled
Pool tracking: Disabled
Force IRQL checking: Disabled
I/O verification: Disabled
Enhanced I/O verification: Disabled
Deadlock detection: Disabled
DMA checking: Disabled
Security checks: Disabled
Force pending I/O requests: Disabled
Low resources simulation: Enabled
IRP Logging: Disabled
Miscellaneous checks: Disabled
Disk integrity checking: Disabled

Low Resources Simulation options:

- Fault injection probability: 1/10000.
- Fail only allocations using pool tags: Tag1 Tag2.
- Simulate low resources conditions only in applications: test1.exe test2.exe.
- Boot time delay: 2 minutes.

Verified drivers:

blah.sys
```









