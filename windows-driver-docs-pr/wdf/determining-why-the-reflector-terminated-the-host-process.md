---
title: 确定反射器终止主机进程的原因
description: 本主题介绍如何分析该发送程序终止驱动程序主机进程 (WUDFHost.exe) 的原因。
ms.assetid: c80b117b-597a-494a-bc28-5a918d2a9279
keywords:
- 调试方案 WDK UMDF，reflector 终止主机进程
- UMDF WDK，调试方案，reflector 终止主机进程
- UMDF WDK reflector 终止主机进程
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ac2975568da83e4c0e28027637ff22d524a732f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377421"
---
# <a name="determining-why-the-reflector-terminated-the-host-process"></a>确定反射器终止主机进程的原因


本主题介绍如何分析该发送程序终止驱动程序主机进程 (WUDFHost.exe) 的原因。

反射器终止主机进程的最常见原因是 UMDF 到期[承载进程超时](how-umdf-enforces-time-outs.md)。

## <a name="using-dump-files"></a>使用转储文件


对于许多崩溃转储文件的详细信息是不足以确定发生终止的原因。 若要查看转储文件信息，请执行以下步骤：

1.  在 %windir%中找到最新的.dmp 文件\\system32\\LogFiles\\WUDF 目录。

    **请注意**  UMDF 2.15 从开始，日志目录是 *%programdata%* \\Microsoft\\WDF。

     

2.  通过使用以下命令将最新的.dmp 文件加载到调试器中：
    ```cpp
    WinDbg -z <path to the .dmp file>
    ```

3.  在终止时，请查看线程的状态。

## <a name="using-the-debugger"></a>使用调试器


在其他情况下，可能需要将附加到实时的内核模式目标，以确定该发送程序终止主机进程的原因。 若要设置你的调试会话，请按照中所述的步骤[如何启用调试 UMDF 驱动程序的](enabling-a-debugger.md#kd)。

一旦建立连接之后，通过使用显示未完成的 Irp [ **！ wdfkd.wdfumirps** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wdfkd-wdfumirps) UMDF 调试器扩展 ([ **！ wudfext.umirps**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-wudfext-umirps)对于 UMDF 版本 1)。

-   如果 PnP IRP 或 power IRP 处于挂起状态，确定为什么驱动程序会导致 IRP 通过检查在主机进程的线程挂起。

    可以使用[ **！ 过程**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-process)扩展来检查在主机进程中运行的线程。 **0x1f**标志值显示为每个线程的堆栈跟踪。

    **!process** *&lt;process addr&gt;* **0x1f**

-   如果您的驱动程序未快速完成取消的 IRP，确定 IRP 已被取消并且为什么它尚未完成。
-   如果清除或关闭 IRP 处于挂起状态，确定为什么 IRP 需要长时间来处理。

 

 





