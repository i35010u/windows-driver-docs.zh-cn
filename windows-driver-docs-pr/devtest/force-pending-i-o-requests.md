---
title: 强制挂起 I/O 请求
description: 强制挂起 I/O 请求
keywords:
- "\"强制挂起 i/o 请求\" 选项 WDK 驱动程序验证程序"
- STATUS_PENDING WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6f0154231c0a8c527d8f1948f7d6e219dd74409
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831581"
---
# <a name="force-pending-io-requests"></a>强制挂起 I/O 请求


"强制挂起 i/o 请求" 选项会随机返回状态 \_ "挂起"，以响应驱动程序对 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)的调用。 此选项将测试驱动程序的逻辑，以响应 \_ **IoCallDriver** 中的状态挂起返回值。

只有 Windows Vista 和更高版本的 Windows 操作系统才支持此选项。

**警告**   不要对驱动程序使用此选项，除非您对驱动程序的操作有详细了解，并且已经验证驱动程序设计为处理 \_ 从其所有调用到 **IOCALLDRIVER** 的状态待定返回值。 如果驱动程序上运行此选项，而该驱动程序未设计为处理 \_ 所有调用的挂起状态，则可能会导致崩溃、内存损坏和异常系统行为，这可能很难进行调试或纠正。

 

### <a name="span-idwhy_use_force_pending_i_o_requests_spanspan-idwhy_use_force_pending_i_o_requests_spanwhy-use-force-pending-io-requests"></a><span id="why_use_force_pending_i_o_requests_"></span><span id="WHY_USE_FORCE_PENDING_I_O_REQUESTS_"></span>为什么使用强制挂起 i/o 请求？

驱动程序堆栈中较高级别的驱动程序调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) ，以便将 IRP 向下传递到驱动程序堆栈中较低级别的驱动程序。 用于接收 IRP 的低级驱动程序中的驱动程序调度例程可以立即完成 IRP，或返回状态 " \_ 挂起"，并在以后完成 irp。

通常，调用方必须准备好处理任一结果。 但是，因为大多数调度例程会立即处理 IRP，所以 \_ 调用方中的状态挂起逻辑通常不会执行，并且可能不会检测到严重的逻辑错误。 "强制挂起 i/o 请求" 选项会截获对 **IoCallDriver** 的调用，并返回状态 " \_ 挂起" 以测试调用驱动程序的不常使用的逻辑。

### <a name="span-idwhen_do_you_use_force_pending_i_o_requests_spanspan-idwhen_do_you_use_force_pending_i_o_requests_spanwhen-do-you-use-force-pending-io-requests"></a><span id="when_do_you_use_force_pending_i_o_requests_"></span><span id="WHEN_DO_YOU_USE_FORCE_PENDING_I_O_REQUESTS_"></span>何时使用强制挂起 i/o 请求？

在运行此测试之前，请查看驱动程序设计和源代码，并确认该驱动程序旨在处理 \_ 其所有 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 调用的挂起状态。

许多驱动程序设计为不处理对 \_ **IoCallDriver** 的所有调用的状态。 它们可能会将 IRP 发送到特定的已知驱动程序，该驱动程序保证会立即完成 IRP。 \_向不处理驱动程序的驱动程序发送挂起状态可能导致驱动程序和系统崩溃和内存损坏。

### <a name="span-idhow_should_drivers_handle_status_pending_spanspan-idhow_should_drivers_handle_status_pending_spanhow-should-drivers-handle-status_pending"></a><span id="how_should_drivers_handle_status_pending_"></span><span id="HOW_SHOULD_DRIVERS_HANDLE_STATUS_PENDING_"></span>驱动程序应如何处理 \_ 挂起状态？

调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 的较高级别的驱动程序必须处理状态 \_ 挂起的返回值，如下所示：

-   在调用 **IoCallDriver** 之前，驱动程序必须调用 [**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest) 来安排对 IRP 的同步处理。

-   如果 **IoCallDriver** 返回状态 \_ "挂起"，则驱动程序必须通过对指定的事件调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 来等待 IRP 完成。

-   驱动程序必须预计 IRP 可能在 i/o 管理器发出事件信号之前被释放。

-   调用 **IoCallDriver** 后，调用方无法引用 IRP。

### <a name="span-idwhich_errors_does_force_pending_i_o_request_detect_spanspan-idwhich_errors_does_force_pending_i_o_request_detect_spanwhich-errors-does-force-pending-io-request-detect"></a><span id="which_errors_does_force_pending_i_o_request_detect_"></span><span id="WHICH_ERRORS_DOES_FORCE_PENDING_I_O_REQUEST_DETECT_"></span>强制挂起 i/o 请求检测哪些错误？

"强制挂起 i/o 请求" 选项检测驱动程序中调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 并收到状态 "等待返回值" 的下列错误 \_ ：

-   驱动程序不会调用 **IoBuildSynchronousFsdRequest** 来安排同步处理。

-   驱动程序未调用 **KeWaitForSingleObject**。

-   在调用 **IoCallDriver** 之后，驱动程序将引用 IRP 结构中的值。 在调用 **IoCallDriver** 之后，较高级别的驱动程序将无法访问 irp，除非它已设置完成例程，然后仅在所有较低级别的驱动程序都完成 IRP 时才访问。 如果已释放 IRP，驱动程序会崩溃。

-   驱动程序未正确调用相关函数。 例如，驱动程序调用 **KeWaitForSingleObject** ，并将一个句柄传递到 (的 *对象* 参数) 的事件，而不是将指针传递到事件对象。

-   驱动程序等待错误的事件。 例如，驱动程序调用 **IoSetCompletionRoutine**，但会等待由其自己的完成例程发出信号的内部事件，而不是等待 irp 事件，该事件是在完成 irp 后由 I/o 管理器发出的。

### <a name="span-idforce_pending_i_o_requests_changes_introduced_in_windows_7spanspan-idforce_pending_i_o_requests_changes_introduced_in_windows_7spanspan-idforce_pending_i_o_requests_changes_introduced_in_windows_7spanforce-pending-io-requests-changes-introduced-in-windows-7"></a><span id="Force_Pending_I_O_Requests_Changes_Introduced_in_Windows_7"></span><span id="force_pending_i_o_requests_changes_introduced_in_windows_7"></span><span id="FORCE_PENDING_I_O_REQUESTS_CHANGES_INTRODUCED_IN_WINDOWS_7"></span>Windows 7 中引入的强制挂起的 i/o 请求更改

从 Windows 7 开始，"强制挂起 i/o 请求" 选项在强制执行 \_ 已验证驱动程序的状态 "挂起代码路径" 时更有效。 在早期的 Windows 版本中，驱动程序验证器仅在该 IRP 的第一个 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 执行时强制延迟 IRP 完成。 这意味着验证 Driver1 的有效性可以通过同一设备堆栈中的 Driver2 行为来减少。 Driver2 可能会等待同步完成，然后从其调度例程返回到 Driver1。 在 i/o 请求回退到完成路径上经过验证的驱动程序之前，IRP 完成的强制延迟精确发生。 这意味着已 \_ 验证驱动程序的状态 "挂起代码路径" 确实会执行，并且已验证的驱动程序会在完成时体验延迟。

### <a name="span-idactivating_this_optionspanspan-idactivating_this_optionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

若要激活强制挂起 i/o 请求，还必须激活 [I/o 验证](i-o-verification.md)。 可以通过使用驱动程序验证器管理器或 Verifier.exe 命令行为一个或多个驱动程序激活 "强制挂起的 i/o 请求" 选项。 有关详细信息，请参阅 [选择驱动程序验证程序选项](selecting-driver-verifier-options.md)。

只有 Windows Vista 和更高版本的 Windows 支持 "强制挂起 i/o 请求" 选项。

-   **在命令行中**

    若要激活强制挂起 i/o 请求，请使用0x210 的标志值或将0x210 添加到标志值。 此值 (0x10) 激活 i/o 验证，并强制 (0x200) 挂起 i/o 请求。

    例如：

    ```
    verifier /flags 0x210 /driver MyDriver.sys
    ```

    选项将在下一次启动后处于活动状态。

    如果尝试仅 (verifier/flags 0x200) 上激活强制挂起的 i/o 请求，驱动程序验证程序会自动启用强制挂起 i/o 请求 (0x200) 和 [I/o 验证](i-o-verification.md)。

    还可以通过将/volatile 参数添加到命令，来激活和停用强制挂起 i/o 请求，而无需重新启动计算机。 例如：

    ```
    verifier /volatile /flags 0x210 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时，此设置会丢失。 有关详细信息，请参阅 [使用可变设置](using-volatile-settings.md)。

-   **使用驱动程序验证器管理器**

    1.  启动驱动程序验证器管理器。 在命令提示符窗口中键入 **Verifier** 。
    2.  选择 " **为代码开发人员 (创建自定义设置")**，然后单击 " **下一步**"。
    3.  选择 " **从完整列表中选择单个设置**"。
    4.  选择 [I/o 验证](i-o-verification.md) 并强制挂起 i/o 请求。

    如果只选择 " **强制挂起 I/o 请求**"，驱动程序验证器管理器会提醒你需要进行 [i/o 验证](i-o-verification.md) ，并提供为你启用该验证。

### <a name="span-idviewing_the_resultsspanspan-idviewing_the_resultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>查看结果

若要查看强制挂起 i/o 请求测试的结果，请使用带有标志值0x40 的 **！ verifier** 调试器扩展。

有关 **！ verifier** 的信息，请参阅 *Windows 调试工具* 文档中的 **！ verifier** 主题。

如果测试计算机因强制挂起 i/o 请求测试而崩溃，则可以使用 **！ verifier 40** 命令查找原因。 在当前的堆栈跟踪中，查找驱动程序最近使用的 IRP 的地址。 例如，如果使用 **kP** 命令显示线程的堆栈帧，则可以在当前堆栈跟踪的函数参数中找到 IRP 地址。 然后，运行 **！ verifier 40** 并查找 IRP 的地址。 最近的强制挂起堆栈跟踪显示在显示的顶部。

例如，以下 Pci.sys 的堆栈跟踪显示其对强制挂起 i/o 请求的响应。 该测试不会揭示 Pci.sys 逻辑中的任何错误。

```
kd> !verifier 40
# Size of the log is 0x40
========================================================
IRP: 8f84ef00 - forced pending from stack trace:

     817b21e4 nt!IovpLocalCompletionRoutine+0xb2
     81422478 nt!IopfCompleteRequest+0x15c
     817b2838 nt!IovCompleteRequest+0x9c
     84d747df acpi!ACPIBusIrpDeviceUsageNotification+0xf5
     84d2d36c acpi!ACPIDispatchIrp+0xe8
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     817c6a9d nt!ViFilterDispatchPnp+0xe9
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84fed489 pci!PciCallDownIrpStack+0xbf
     84fde1cb pci!PciDispatchPnpPower+0xdf
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     817c6a9d nt!ViFilterDispatchPnp+0xe9
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84ff2ff5 pci!PciSendPnpIrp+0xbd
 84fec820 pci!PciDevice_DeviceUsageNotification+0x6e
     84fde1f8 pci!PciDispatchPnpPower+0x10c
 817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84d76ce2 acpi!ACPIFilterIrpDeviceUsageNotification+0x96
     84d2d36c acpi!ACPIDispatchIrp+0xe8
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
     84f7f16c PCIIDEX!PortWdmForwardIrpSynchronous+0x8e
     84f7b2b3 PCIIDEX!GenPnpFdoUsageNotification+0xcb
     84f7d301 PCIIDEX!PciIdeDispatchPnp+0x45
     817b258f nt!IovCallDriver+0x19d
     8142218e nt!IofCallDriver+0x1c
```

堆栈跟踪显示 *Acpi.sys* 尝试完成 IRP 8f84ef00。 驱动程序验证程序强制执行延迟的完成，因此 *Acpi.sys* 返回的状态为 "正在 \_ 等待 **pci！PciCallDownIrpStack**。 如果此调用导致崩溃，驱动程序所有者需要查看 pci 的源代码 **！PciCallDownIrpStack** 并对其进行修订，以处理正确的状态 \_ 。

 

