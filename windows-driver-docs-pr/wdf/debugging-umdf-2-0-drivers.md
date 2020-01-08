---
title: 排查 UMDF 2.0 驱动程序崩溃问题
description: 从用户模式驱动程序框架（UMDF）版本2开始，你可以使用 Wdfkd 中实现的调试器扩展命令的子集来调试 UMDF 驱动程序。
ms.assetid: df1bfc10-379b-457f-a9c8-40fa10048f81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4336f7b007fe1d03f5f2fb902658779d24d5f84d
ms.sourcegitcommit: 9355a80229bb2384dd45493d36bdc783abdd8d7a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2020
ms.locfileid: "75694241"
---
# <a name="troubleshooting-umdf-20-driver-crashes"></a>排查 UMDF 2.0 驱动程序崩溃问题


从用户模式驱动程序框架（UMDF）版本2开始，你可以使用 Wdfkd 中实现的调试器扩展命令的子集来调试 UMDF 驱动程序。 本主题介绍了你可能会启动哪些命令来解决 UMDF 驱动程序问题。

##  <a name="determining-why-a-umdf-20-driver-crashed"></a>确定 UMDF 2.0 驱动程序崩溃的原因


如果驱动程序主机进程已终止，则您的驱动程序在回调中可能出现问题，导致超出了[主机超时](how-umdf-enforces-time-outs.md)阈值。 在这种情况下，反射器将终止驱动程序主机进程。

若要进行调查，请首先按照[如何启用 UMDF 驱动程序调试](enabling-a-debugger.md)中所述设置内核模式调试会话。 我们强烈建议使用连接到测试系统的内核调试器并在 WUDFHost 上启用[应用程序验证工具（AppVerif）](../debugger/debugger-download-tools.md) ，来完成 UMDF 驱动程序的开发和测试。 使用以下命令，附加内核调试器，然后重新启动。

```cpp
AppVerif –enable Heaps Exceptions Handles Locks Memory TLS Leak –for WudfHost.exe
```

- 如果设置了**HostFailKdDebugBreak** （默认情况下应在 Windows 8 中启用此功能），则在超出超时阈值时，反射器将进入内核模式调试器。 在调试器输出中，你将看到有关如何开始的几个建议，包括你可以单击的链接。 例如：

  ```cpp
  **** Problem detected in UMDF driver "WUDFOsrUsbFx2". !process 0xFFFFE0000495B080 0x1f, !devstack 0xFFFFE000032BFA10, Problem code 3 ****
  **** Dump UMDF driver image name and stack: !wdfkd.wdfumdevstack 0x000000BEBB49AE20
  **** Dump UM Irps for this stack: !wdfkd.wdfumirps 0x000000BEBB49AE20
  **** Dump UMDF trace log: !wmitrace.logdump WUDFTrace
  **** Helpful UMDF debugger extension commands: !wdfkd.wdfhelp
  **** Note that driver host process may get terminated if you go past this break, making it difficult to debug the problem!
  ```

- 使用[ **！进行分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)以显示有关失败的信息以及可以尝试的其他 UMDF 扩展命令。
- 使用[ **！ process 0 0x1f wudfhost**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process)列出所有 wudfhost 驱动程序主机进程，包括线程堆栈信息。

  你还可以使用！ wdfkd，wdfumtriage 和[ **！ wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfldr)显示当前绑定到 WDF 的所有驱动程序。 单击 UMDF 驱动程序的映像名称时，调试器将显示托管进程的地址。 然后，你可以单击该进程地址以显示特定于该流程的信息。

- 如有必要，请使用[ **。 process/r/P*进程*** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process--set-process-context-)将进程上下文切换到托管驱动程序的 Wudfhost 进程的上下文。 使用[**forcedecodeuser**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-cache--set-cache-size-)和**lmu**来验证驱动程序是否承载于当前进程中。
- 检查线程调用堆栈（[ **！线程*地址*** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-thread)）以确定驱动程序回调是否超时。查看线程的滴答计数。 在 Windows 8.1 中，反射器会在一分钟后超时。
- 使用[ **！ wdfkd Wdfdriverinfo MyDriver**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdriverinfo) ，以详细形式显示设备树。 然后单击[ **！ wdfdevice**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevice)。 此命令显示详细电源、电源策略和即插即用（PnP）状态信息。
- 使用[ **！ wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps)查找挂起的 irp。
- 使用[ **！ wdfkd**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfdevicequeues)检查驱动程序队列的状态。
- 在内核模式调试会话中，可使用[ **！ Logdump WudfTrace**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wmitrace-logdump)显示跟踪日志。 wmitrace

## <a name="displaying-the-umdf-20-ifr-log"></a>显示 UMDF 2.0 IFR 日志


在内核模式调试会话中，可以使用[ **！ wdfkd wdflogdump**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdflogdump)扩展命令显示 Windows 驱动程序框架（WDF）正在进行的记录器（IFR）日志记录（如果可用）。

## <a name="finding-memory-dump-files"></a>查找内存转储文件


有关查找用户模式转储文件的信息，请参阅[确定反射器为何终止了主机进程](determining-why-the-reflector-terminated-the-host-process.md)。 有关如何设置**LogMinidumpType**注册表值以指定存储在小型转储文件中的信息类型的信息，请参阅[在 UMDF 驱动程序中使用 WPP 软件跟踪](using-wpp-software-tracing-in-umdf-drivers.md)。







