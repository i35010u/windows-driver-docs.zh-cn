---
title: 资源不足模拟
description: 资源不足模拟
keywords:
- 低资源模拟选项 WDK 驱动程序验证程序
- 低内存检查 WDK 驱动程序验证程序
- 内存不足检查 WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7dadda53c95d26770e31e5140f7df2146d33f66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826689"
---
# <a name="low-resources-simulation"></a>资源不足模拟

## <span id="ddk_low_resources_simulation_tools"></span><span id="DDK_LOW_RESOURCES_SIMULATION_TOOLS"></span>

当 "低资源" 模拟选项 (在 Windows 8.1) 处于活动状态时调用 " *随机低资源" 模拟* 时，驱动程序验证器会失败驱动程序的内存分配的随机实例，这可能是因为驱动程序在内存不足的计算机上运行。 这会测试驱动程序能否正确响应内存不足的问题和其他资源不足的情况。

低资源模拟测试无法通过对多个不同函数（包括 [**ExAllocatePoolWithXXX**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)、 [**MmGetSystemAddressForMdlSafe**](../kernel/mm-bad-pointer.md)、 [**MmProbeAndLockPages**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmprobeandlockpages)、 [**MmMapLockedPagesSpecifyCache**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmaplockedpagesspecifycache)和 [**MmMapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace)）的调用来请求分配。

从 Windows Vista 开始，低资源模拟测试还会将故障注入到 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)、 [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)、 [**IoAllocateWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateworkitem)、 [**IoAllocateErrorLogEntry**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateerrorlogentry)、 [**MmAllocateContiguousMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)、 [**MmAllocateContiguousMemorySpecifyCache**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)、 [**MmAllocatePagesForMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdl)和 [**MmAllocatePagesForMdlEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)。 此外，从 Windows Vista 开始，当低资源模拟处于启用状态时，如果将 *可报警* 参数设置为 **TRUE** ，则对 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)或 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)的调用可能会在 \_ 非特权进程的上下文中运行时返回状态警报。 这会模拟来自同一非特权应用程序中其他线程的可能的线程警报。

低资源模拟测试还将错误注入到以下 GDI 函数： [**EngAllocMem**](/windows/win32/api/winddi/nf-winddi-engallocmem)、 [**EngAllocUserMem**](/windows/win32/api/winddi/nf-winddi-engallocusermem)、 [**EngCreateBitmap**](/windows/win32/api/winddi/nf-winddi-engcreatebitmap)、 [**EngCreateDeviceSurface**](/windows/win32/api/winddi/nf-winddi-engcreatedevicesurface)、 [**EngCreateDeviceBitmap**](/windows/win32/api/winddi/nf-winddi-engcreatedevicebitmap)、 [**EngCreatePalette**](/windows/win32/api/winddi/nf-winddi-engcreatepalette)、 [**EngCreateClip**](/windows/win32/api/winddi/nf-winddi-engcreateclip)、 [**EngCreatePath**](/windows/win32/api/winddi/nf-winddi-engcreatepath)、 [**EngCreateWnd**](/windows/win32/api/winddi/nf-winddi-engcreatewnd)、 [**EngCreateDriverObj**](/windows/win32/api/winddi/nf-winddi-engcreatedriverobj)、 [**BRUSHOBJ \_ pvAllocRbrush**](/windows/win32/api/winddi/nf-winddi-brushobj_pvallocrbrush)和 [**CLIPOBJ \_ ppoGetPath**](/windows/win32/api/winddi/nf-winddi-clipobj_ppogetpath)。

在 windows 7 和更高版本的 Windows 操作系统中，"低资源" 模拟选项支持使用以下内核 Api 分配的内存：

-   [**IoAllocateMdl**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatemdl)

-   [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 以及可以 (IRP) 数据结构分配 i/o 请求包的其他例程

-   [**RtlAnsiStringToUnicodeString**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlansistringtounicodestring) 和其他运行时库 (RTL) 字符串例程

-   [**IoSetCompletionRoutineEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcompletionroutineex)

从 Windows 8.1 开始，低资源模拟选项还会使对 MmAllocateNodePagesForMdlEx 的调用所请求的分配失败。 此外，对于某些函数，驱动程序验证程序现在使用随机模式填充分配的内存。 但仅适用于函数返回未初始化的内存的情况。 这些函数包括：

-   [**MmAllocatePagesForMdlEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatepagesformdlex)
-   MmAllocateNodePagesForMdlEx
-   [**MmAllocateContiguousMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemory)
-   [**MmAllocateContiguousMemorySpecifyCache**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycache)
-   [**MmAllocateContiguousMemorySpecifyCacheNode**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousmemoryspecifycachenode)
-   [**MmAllocateContiguousNodeMemory**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmallocatecontiguousnodememory)
-   [**MmAllocateNonCachedMemory**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmallocatenoncachedmemory)

### <a name="span-idcustom_settings_for_low_resources_simulationspanspan-idcustom_settings_for_low_resources_simulationspancustom-settings-for-low-resources-simulation"></a><span id="custom_settings_for_low_resources_simulation"></span><span id="CUSTOM_SETTINGS_FOR_LOW_RESOURCES_SIMULATION"></span>低资源模拟的自定义设置

在 Windows Vista 和更高版本的 Windows 上，你可以指定以下自定义设置。

-   给定分配失败的 **概率**。 默认值为6%。

-   受影响的 **应用程序**。 此设置将插入的失败分配限制到指定的应用程序。 默认情况下，将影响所有分配。

-   受影响的 **池标记**。 此设置将插入的故障限制为具有指定池标记的分配。 默认情况下，将影响所有分配。

-   在分配失败之前 **延迟** (分钟) 。 此延迟允许系统在错误注入之前启动并稳定。 默认值为8分钟。

在 Windows Vista 之前的操作系统上，不能自定义这些设置。 操作系统使用默认值。

### <a name="span-idlow_resources_simulation_without_rebootingspanspan-idlow_resources_simulation_without_rebootingspanlow-resources-simulation-without-rebooting"></a><span id="low_resources_simulation_without_rebooting"></span><span id="LOW_RESOURCES_SIMULATION_WITHOUT_REBOOTING"></span>低资源模拟，无需重新启动

您可以在 Windows 2000 和更高版本的 Windows 上激活低资源模拟，而无需使用 **/volatile** 参数重新启动计算机。 设置将立即生效，但如果关闭或重新启动计算机，则会丢失这些设置。

还可以通过省略 **/volatile** 参数，将低资源模拟设置存储在注册表中。 仅当重新启动计算机时，这些设置才有效，但在你更改它们之前，这些设置将保持有效。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活低资源模拟选项。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

-   **在命令行中**

    在命令行中，低资源模拟选项由 **位 2 (0x4)** 表示。 若要激活低资源模拟，请使用值为0x4 的标志值或将0x4 添加到 flags 值。 例如：

    ```
    verifier /flags 0x4 /driver MyDriver.sys
    ```

    选项将在下一次启动后处于活动状态。

    在 Windows Vista 和更高版本的 Windows 上，可以使用 */faults* 参数或标志值 **0X4** 激活低资源模拟。 若要修改低资源模拟的设置，必须使用 **/faults**。 例如：

    ```
    verifier /faults /driver MyDriver.sys
    ```

    在 Windows 2000 和更高版本的 Windows 上，还可以通过将 **/volatile** 参数添加到命令，来激活和停用低资源模拟，无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x4 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

    在 Windows Vista 上，你可以使用 **/faults** 参数来表示使用 **/Volatile** 参数的低资源模拟，以表示在不重新启动的情况下有效的设置。 将显示设置更改。 例如：

    ```
    0>  verifier /volatile /faults /adddriver MyDriver.sys
    New Low Resources Simulation options:

    - Use default fault injection probability.
    - Allocations using any pool tag can be failed.
    - Simulate low resources conditions in any application.

    The new settings are in effect until you restart this computer
    or change them again.
    ```

-   **使用驱动程序验证器管理器**
    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")**，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 **低资源模拟**。

### <a name="span-idcustomizing_the_settings__windows_vista_and_later_spanspan-idcustomizing_the_settings__windows_vista_and_later_spancustomizing-the-settings-windows-vista-and-later"></a><span id="customizing_the_settings__windows_vista_and_later_"></span><span id="CUSTOMIZING_THE_SETTINGS__WINDOWS_VISTA_AND_LATER_"></span>自定义 Windows Vista 和更高版本 (设置) 

从 Windows Vista 开始，你可以更改 "低资源模拟" 选项的 "延迟"、"概率"、"应用程序" 和 "池标记" 属性的默认设置。 可以通过使用驱动程序验证程序管理器或 Verifier.exe 命令行来更改这些设置。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

在命令行中，这些设置的语法如下所示：

**验证** \[ 程序 **/volatile** \]**/faults** \[*概率* |*PoolTags* |*应用程序* |*DelayMins* \] DelayMins \[**/driver** |*DriverList*\]

**注意**  自定义设置参数必须按显示的顺序出现。 如果省略某个值，请键入引号以保存其位置。



**子参数**

- **/faults**

  启用驱动程序验证器中的低资源模拟选项。  (不能将/flags 0x4 用于自定义设置子参数。 ) 

- *概率*

  指定驱动程序验证程序在给定分配中将失败的概率。 以十进制或十六进制格式键入数字 () ，表示驱动程序验证程序在分配失败的几率（10000）。 默认值为600，表示600/10000 或6%。

- *PoolTags*

  限制驱动程序验证程序无法通过指定的池标记分配的分配数。 您可以使用通配符 ( * *\** _) 来表示多个池标记。 若要列出多个池标记，请用空格分隔标记。 默认情况下，所有分配都可能失败。

- _Applications *

  限制驱动程序验证程序可为指定程序分配的分配数。 键入可执行文件的名称。 若要列出程序，请用空格分隔程序名称。 默认情况下，所有分配都可能失败。

- *DelayMins*

  指定引导后的分钟数，在此期间，驱动程序验证程序不会有意失败任何分配。 此延迟允许在测试开始之前加载驱动程序并使系统稳定。 以十进制或十六进制格式键入数字 () 。 默认值为 8 (分钟) 。

例如，以下命令启用低资源模拟，其概率为 10% (1000/10000) ，而池标记、Tag1 和 Fred 的延迟为5分钟，Notepad.exe。

```
verifier /faults 1000 "Tag1 Fred" Notepad.exe 5
```

下面的命令通过默认值启用低资源模拟，只不过它将延迟延长到10分钟。

```
verifier /faults "" "" "" 0xa
```

**使用驱动程序验证器管理器**

1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
2.  选择 " **为代码开发人员 (创建自定义设置")**，然后单击 " **下一步**"。

3.  选择 " **从完整列表中选择单个设置**"。

4.  选择 **低资源模拟**，并单击 " **下一步"。**

5.  根据需要更改 "延迟"、"概率"、"应用程序" 和 "池标记" 属性的设置。

### <a name="span-idviewing_the_resultsspanspan-idviewing_the_resultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>查看结果

可以通过显示驱动程序验证器 *错误注入* 的全局计数器来监视驱动程序验证程序有意失败资源分配的次数。 此计数器显示自上次启动以来驱动程序验证程序特意失败的资源分配总数。

你可以在命令行 (**/query**) 或驱动程序验证器管理器的命令行中查看驱动程序验证程序日志文件中的此计数器 (**/log**) 。 在 Windows 2000 中，若要查看全局计数器，请选择 "**全局计数器**" 选项卡。在更高版本的 Windows 中，选择 **"显示有关当前已验证的驱动程序任务的信息**"，**然后按两次。** 有关详细信息，请参阅 [监视全局计数器](monitoring-global-counters.md)。

您还可以通过使用 **！ verifier** 调试器扩展来显示有意失败分配的数量以及 (计算概率) 的总分配数。 下面的示例演示了 **！ verifier** 输出的示例。

在此示例中， **插入随机低资源 API 故障** 表示已启用低资源模拟。 **资源分配故意** 表示有意失败的分配数，而 **池分配尝试** 表示分配总数。

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

若要为驱动程序验证器显示最近失败的分配的堆栈跟踪，请在内核调试器中使用 **！ Verifier 4** 。

下面的示例演示 **！ verifier 4** 的输出示例。 默认情况下， **！ verifier 4** 显示来自四个最近失败的分配的堆栈跟踪，但你可以使用其 *数量* 参数增加显示的堆栈跟踪数。 例如，！ verifier 0x80 显示128最近失败的分配。

在此示例中，请注意，验证程序已截获并替换驱动程序对 **ExAllocatePoolWithTag** 的调用。 驱动程序崩溃的最常见原因之一是，驱动程序尝试分配内存，然后使用分配函数返回的指针，然后再验证它是否不 **为 NULL**。

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

低资源模拟测试的经验表明，大多数驱动程序崩溃都是由最新失败的分配造成的。 在上面的示例中，崩溃在 **win32k.sys！GreEnableEUDC**。 检查分配路径中的代码以找出崩溃的原因。

有关 **！ verifier** 的信息，请参阅 *Windows 调试工具* 文档。

若要在命令行中查看注册表中的设置，请使用 **/querysettings** 选项。 例如：

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
