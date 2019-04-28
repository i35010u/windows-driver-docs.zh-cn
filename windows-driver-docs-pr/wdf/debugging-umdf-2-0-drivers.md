---
title: 排查 UMDF 2.0 驱动程序崩溃问题
description: 从在用户模式驱动程序框架 (UMDF) 版本 2 开始，可以使用调试器扩展命令在 Wdfkd.dll 中实现的子集来调试 UMDF 驱动程序。
ms.assetid: df1bfc10-379b-457f-a9c8-40fa10048f81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ba636c96e7cbf3e38afb96f62ac069d4ac50f29a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330865"
---
# <a name="troubleshooting-umdf-20-driver-crashes"></a>排查 UMDF 2.0 驱动程序崩溃问题


从在用户模式驱动程序框架 (UMDF) 版本 2 开始，可以使用调试器扩展命令在 Wdfkd.dll 中实现的子集来调试 UMDF 驱动程序。 本主题介绍的命令可能与启动解决 UMDF 驱动程序问题。

##  <a name="determining-why-a-umdf-20-driver-crashed"></a>确定为什么 2.0 UMDF 驱动程序崩溃


如果驱动程序主机进程将终止，您的驱动程序可能会导致回调中出现问题[主机超时](how-umdf-enforces-time-outs.md)正在超过了阈值。 在这种情况下，该发送程序将终止驱动程序主机进程。

若要调查，先设置内核模式调试会话中所述[如何启用调试 UMDF 驱动程序的](enabling-a-debugger.md)。

- 如果**HostFailKdDebugBreak**设置到内核模式调试程序时超出了超时阈值 reflector 分页符。 在调试器输出中，您将看到多个建议如何开始，其中包括你可以单击的链接。 例如：

  ```cpp
  **** Problem detected in UMDF driver "WUDFOsrUsbFx2". !process 0xFFFFE0000495B080 0x1f, !devstack 0xFFFFE000032BFA10, Problem code 3 ****
  **** Dump UMDF driver image name and stack: !wdfkd.wdfumdevstack 0x000000BEBB49AE20
  **** Dump UM Irps for this stack: !wdfkd.wdfumirps 0x000000BEBB49AE20
  **** Dump UMDF trace log: !wmitrace.logdump WUDFTrace
  **** Helpful UMDF debugger extension commands: !wdfkd.wdfhelp
  **** Note that driver host process may get terminated if you go past this break, making it difficult to debug the problem!
  ```

- 使用[ **！ 分析**](https://msdn.microsoft.com/library/windows/hardware/ff562112)以显示你可以尝试故障和其他 UMDF 扩展命令有关的信息。
- 使用[ **！ 进程 0 0x1f wudfhost.exe** ](https://msdn.microsoft.com/library/windows/hardware/ff564717)若要列出所有 Wudfhost.exe 驱动程序主机进程，包括线程的堆栈信息。

  此外可以使用[ **！ wdfkd.wdfldr** ](https://msdn.microsoft.com/library/windows/hardware/ff565803)可以显示当前绑定到 WDF 的所有驱动程序。 当单击 UMDF 驱动程序的映像名称时，调试器将显示承载进程的地址。 然后可以单击以显示信息特定于该进程的进程地址。

- 如有必要，使用[ **.process /r/p*进程*** ](https://msdn.microsoft.com/library/windows/hardware/ff564723)进程上下文切换到的 Wudfhost 进程承载您的驱动程序。 使用[ **.cache forcedecodeuser** ](https://msdn.microsoft.com/library/windows/hardware/ff562180)并**lmu**以验证您的驱动程序位于当前进程中。
- 检查线程调用堆栈 ([**！ 线程*地址***](https://msdn.microsoft.com/library/windows/hardware/ff565440)) 以确定驱动程序回调操作已超时。查看线程的计时周期计数。 在 Windows 8.1 中该发送程序将会超时后一分钟。
- 使用[ **！ wdfkd.wdfdriverinfo MyDriver.dll 0x10** ](https://msdn.microsoft.com/library/windows/hardware/ff565724)详细窗体中显示设备树。 然后单击[ **！ wdfdevice**](https://msdn.microsoft.com/library/windows/hardware/ff565703)。 此命令显示详细的电源、 电源策略和插即用 (PnP) 的状态信息。
- 使用[ **！ wdfkd.wdfumirps** ](https://msdn.microsoft.com/library/windows/hardware/dn265384)要查找挂起的 Irp。
- 使用[ **！ wdfkd.wdfdevicequeues** ](https://msdn.microsoft.com/library/windows/hardware/ff565715)检查驱动程序的队列的状态。
- 在内核模式调试会话中，可以使用[ **！ wmitrace.logdump WudfTrace** ](https://msdn.microsoft.com/library/windows/hardware/ff566159)显示跟踪日志。

## <a name="displaying-the-umdf-20-ifr-log"></a>显示 UMDF 2.0 IFR 日志


在内核模式调试会话中，可以使用[ **！ wdfkd.wdflogdump** ](https://msdn.microsoft.com/library/windows/hardware/ff565805)扩展命令以显示 Windows 驱动程序框架 (WDF) 正在进行记录器 (IFR) 日志记录，如果可用。

## <a name="finding-memory-dump-files"></a>查找内存转储文件


请参阅[确定该发送程序终止主机进程的原因](determining-why-the-reflector-terminated-the-host-process.md)有关查找用户模式转储文件的信息。 请参阅[UMDF 驱动程序中使用 WPP 软件跟踪](using-wpp-software-tracing-in-umdf-drivers.md)有关如何设置的信息**LogMinidumpType**注册表值以指定的小型转储文件中存储信息的类型。









