---
title: 强制挂起 I/O 请求
description: 强制挂起 I/O 请求
ms.assetid: 0255fc5c-0e75-4108-ba29-f1a61ce9b0dd
keywords:
- 强制挂起 I/O 请求选项 WDK Driver Verifier
- STATUS_PENDING WDK 驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 980c325c5f1627c2fd18404f34e55b59c433a57c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63387253"
---
# <a name="force-pending-io-requests"></a>强制挂起 I/O 请求


强制挂起 I/O 请求选项随机返回状态\_驱动程序的调用的响应的待决[ **IoCallDriver**](https://msdn.microsoft.com/library/windows/hardware/ff548336)。 此选项测试驱动程序的响应的状态的逻辑\_PENDING 返回值从**IoCallDriver**。

仅在 Windows Vista 和更高版本的 Windows 操作系统上支持此选项。

**谨慎**  不要使用此驱动程序上的选项，除非驱动程序的操作的详细知识，确认该驱动程序旨在处理状态\_PENDING 从所有对其调用都返回值**IoCallDriver**。 运行此选项在驱动程序未设计为处理状态\_PENDING 从所有调用可能会导致崩溃、 内存损坏和异常系统行为的可能很难调试或更正。

 

### <a name="span-idwhyuseforcependingiorequestsspanspan-idwhyuseforcependingiorequestsspanwhy-use-force-pending-io-requests"></a><span id="why_use_force_pending_i_o_requests_"></span><span id="WHY_USE_FORCE_PENDING_I_O_REQUESTS_"></span>为何使用强制挂起 I/O 请求？

驱动程序中的更高级别的驱动程序堆栈调用[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) IRP 到较低级别的驱动程序传入驱动程序堆栈。 接收 IRP 的较低级驱动程序中的驱动程序调度例程可以立即完成 IRP 或返回状态\_PENDING 并在以后完成 IRP。

通常情况下，调用方必须准备好处理任一结果。 但是，因为大多数调度例程处理 IRP 立即状态\_挂起的调用方中的逻辑不是通常已执行并且十分严重错误可能未检测到的逻辑。 强制挂起 I/O 请求选项截获对调用**IoCallDriver** ，并返回状态\_挂起测试调用驱动程序的不常使用的逻辑。

### <a name="span-idwhendoyouuseforcependingiorequestsspanspan-idwhendoyouuseforcependingiorequestsspanwhen-do-you-use-force-pending-io-requests"></a><span id="when_do_you_use_force_pending_i_o_requests_"></span><span id="WHEN_DO_YOU_USE_FORCE_PENDING_I_O_REQUESTS_"></span>何时使用强制挂起 I/O 请求？

在运行此测试之前, 查看驱动程序设计和源代码并确认该驱动程序旨在处理状态\_PENDING 从所有其[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)调用。

许多驱动程序不用于处理状态\_在所有调用的待决**IoCallDriver**。 它们可能会将 IRP 发送到保证立即完成 IRP 的特定的已知驱动程序。 发送状态\_PENDING 到驱动程序无法处理它可能会导致驱动程序和系统崩溃和内存损坏。

### <a name="span-idhowshoulddrivershandlestatuspendingspanspan-idhowshoulddrivershandlestatuspendingspanhow-should-drivers-handle-statuspending"></a><span id="how_should_drivers_handle_status_pending_"></span><span id="HOW_SHOULD_DRIVERS_HANDLE_STATUS_PENDING_"></span>驱动程序应如何处理状态\_PENDING？

调用的更高级别的驱动程序[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336)必须处理状态\_PENDING 返回值，如下所示：

-   然后再调用**IoCallDriver**，该驱动程序必须调用[ **IoBuildSynchronousFsdRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548330)来安排同步处理 IRP。

-   如果**IoCallDriver**将返回状态\_挂起、 驱动程序必须等待的 IRP 完成后通过调用[ **KeWaitForSingleObject** ](https://msdn.microsoft.com/library/windows/hardware/ff553350)上指定事件。

-   该驱动程序必须首先在 I/O 管理器向事件发出信号，可能会释放 IRP 预料。

-   在调用**IoCallDriver**，调用方不能引用 IRP。

### <a name="span-idwhicherrorsdoesforcependingiorequestdetectspanspan-idwhicherrorsdoesforcependingiorequestdetectspanwhich-errors-does-force-pending-io-request-detect"></a><span id="which_errors_does_force_pending_i_o_request_detect_"></span><span id="WHICH_ERRORS_DOES_FORCE_PENDING_I_O_REQUEST_DETECT_"></span>强制挂起 I/O 请求检测到哪些错误？

强制挂起 I/O 请求选项中调用的驱动程序检测到以下错误[ **IoCallDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff548336) ，并接收状态\_PENDING 返回值：

-   该驱动程序不会调用**IoBuildSynchronousFsdRequest**排列为同步处理。

-   该驱动程序不会调用**KeWaitForSingleObject**。

-   该驱动程序之后调用引用 IRP 结构中的值**IoCallDriver**。 在调用**IoCallDriver**，更高级别的驱动程序不能访问 IRP，除非已设置完成例程，然后，仅当较低级别的所有驱动程序已完成 IRP。 如果释放 IRP，驱动程序将崩溃。

-   该驱动程序错误地调用一个相关的函数。 例如，驱动程序调用**KeWaitForSingleObject**并将句柄传递给事件 (作为*对象*参数)，而不是指针传递给一个事件对象。

-   该驱动程序将等待错误事件。 例如，驱动程序调用**IoSetCompletionRoutine**，但在等待由自己完成例程，而不是等待当 IRP 完成时终止的 I/O 管理器的 IRP 事件发送信号的内部事件。

### <a name="span-idforcependingiorequestschangesintroducedinwindows7spanspan-idforcependingiorequestschangesintroducedinwindows7spanspan-idforcependingiorequestschangesintroducedinwindows7spanforce-pending-io-requests-changes-introduced-in-windows-7"></a><span id="Force_Pending_I_O_Requests_Changes_Introduced_in_Windows_7"></span><span id="force_pending_i_o_requests_changes_introduced_in_windows_7"></span><span id="FORCE_PENDING_I_O_REQUESTS_CHANGES_INTRODUCED_IN_WINDOWS_7"></span>强制挂起 I/O 请求更改中引入的 Windows 7

从 Windows 7 开始，强制挂起 I/O 请求选项是更有效地强制执行状态的\_挂起的已验证的驱动程序中的代码路径。 在早期 Windows 版本中，驱动程序验证程序强制延迟，可将 IRP 完成仅当第一个[ **IoCompleteRequest** ](https://msdn.microsoft.com/library/windows/hardware/ff548343)为该 IRP 执行。 这意味着，可以从同一个设备堆栈减少了 Driver2 的行为的验证 Driver1 有效性。 Driver2 可能会等待同步完成之前它从其调度例程返回到 Driver1。 准确地说之前的 I/O 请求返回到完成路径上的已验证驱动程序将回退，将发生 IRP 完成的强制的延迟。 这意味着，状态\_挂起代码真正执行已验证的驱动程序的路径和已验证的驱动程序检测到用户情况中完成的延迟。

### <a name="span-idactivatingthisoptionspanspan-idactivatingthisoptionspanactivating-this-option"></a><span id="activating_this_option"></span><span id="ACTIVATING_THIS_OPTION"></span>激活此选项

若要激活强制挂起 I/O 请求，你必须激活[I/O 验证](i-o-verification.md)。 可以使用驱动程序验证程序管理器或 Verifier.exe 命令行来激活一个或多个驱动程序的强制挂起 I/O 请求选项。 有关详细信息，请参阅[选择 Driver Verifier 选项](selecting-driver-verifier-options.md)。

仅在 Windows Vista 和更高版本的 Windows 上支持强制挂起 I/O 请求选项。

-   **在命令行**

    若要激活强制挂起 I/O 请求，使用 0x210 标志值，或将 0x210 添加到标志值。 此值将激活 I/O 验证 (0x10) 和强制挂起 I/O 请求 (0x200)。

    例如：

    ```
    verifier /flags 0x210 /driver MyDriver.sys
    ```

    在下一次启动后，选项将处于活动状态。

    如果你尝试激活仅强制挂起 I/O 请求 (verifier /flags 0x200)，驱动程序验证程序会自动启用这两个强制挂起 I/O 请求 (0x200) 和[I/O 验证](i-o-verification.md)。

    您还可以激活和停强制挂起 I/O 请求用而无需重启计算机，通过添加 /volatile 命令参数。 例如：

    ```
    verifier /volatile /flags 0x210 /adddriver MyDriver.sys
    ```

    此设置将立即生效，但当你关闭或重新启动计算机时将丢失。 有关详细信息，请参阅[使用易失性设置](using-volatile-settings.md)。

-   **使用驱动程序验证程序管理器**

    1.  启动驱动程序验证器管理器。 类型**Verifier**在命令提示符窗口中。
    2.  选择**创建自定义设置 （适用于代码开发人员）**，然后单击**下一步**。
    3.  选择**从完整的列表中选择单个设置**。
    4.  选择[I/O 验证](i-o-verification.md)和强制挂起 I/O 请求。

    如果仅选择**强制挂起 I/O 请求**，驱动程序验证程序管理器会提醒您， [I/O 验证](i-o-verification.md)是必需的可为您启用它。

### <a name="span-idviewingtheresultsspanspan-idviewingtheresultsspanviewing-the-results"></a><span id="viewing_the_results"></span><span id="VIEWING_THE_RESULTS"></span>查看结果

若要查看强制挂起 I/O 请求测试的结果，请使用 **！ verifier**调试器扩展与 0x40 标志值。

有关信息 **！ verifier**，请参阅 **！ verifier**中的主题*有关 Windows 调试工具*文档。

如果测试计算机崩溃强制挂起 I/O 请求测试的结果，则可以使用 **！ verifier 40**命令查找原因。 在当前堆栈跟踪中，找到最近由您的驱动程序 IRP 的地址。 例如，如果您使用**kP**命令，用于显示线程的堆栈帧，可以查找在当前的堆栈跟踪的函数参数之间的 IRP 地址。 然后，运行 **！ verifier 40**并查找 IRP 的地址。 挂起的堆栈跟踪最新的强制出现在显示的顶部。

例如，下面的堆栈跟踪的 Pci.sys 演示强制挂起 I/O 请求其响应。 测试不会泄露 Pci.sys 逻辑中的任何错误。

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

堆栈跟踪显示*Acpi.sys*尝试完成 IRP 8f84ef00。 驱动程序验证程序强制延迟的完成，因此*Acpi.sys*返回的状态为\_PENDING 到**pci ！PciCallDownIrpStack**。 如果此调用有导致故障发生，驱动程序所有者会需要查看的源代码**pci ！PciCallDownIrpStack**并对其处理状态修订\_PENDING 正确。

 

 





