---
title: 对运行基于 WDTF 的测试时出现的问题进行诊断
description: 若要帮助解决有关运行基于 WDTF 的测试的问题，可以使用调试器。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 074dbed62814f098c9f057b26e61f2d62ce1ec56
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785395"
---
# <a name="diagnosing-problems-running-wdtf-based-tests"></a>对运行基于 WDTF 的测试时出现的问题进行诊断


若要帮助解决有关运行基于 WDTF 的测试的问题，可以使用调试器。

## <a name="diagnose-problems-with-unresponsive-wdtf-based-tests-run-from-visual-studio"></a>诊断 (从 Visual Studio 运行的基于响应 WDTF 的测试的问题) 


1.  配置内核调试器并将其连接到运行基于 WDTF 的测试的计算机。 请参阅 [设置计算机以进行驱动程序部署和测试 (wdk 8.1) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md) 或 [预配用于驱动程序部署和测试 (WDK 8) ](../gettingstarted/provision-a-target-computer-wdk-8-1.md)的计算机。
2.  搜索 Te.exe 进程，并将上下文切换到该进程。 有关 Te.exe 的信息，请参阅 [测试创作和执行框架 (TAEF) ](../taef/index.md)。

    ``` syntax
    !process 0 0 Te.exe 

    PROCESS fffffa80093c6340

    SessionId: 1 Cid: 1320 Peb: 7f6595b3000 ParentCid: 12a0

    DirBase: 21eee000 ObjectTable: fffff8a0035b0a00 HandleCount: 327.

    Image: TE.exe

    ·         .process /p /r fffffa80093c6340

    ·         
    ```

3.  运行 [**！ process**](../debugger/-process.md) 命令来识别在 Te.exe 下运行的线程。

    ``` syntax
    !process fffffa80093c6340
    ```

    在堆栈上查找包含 **WDTF** 的线程 \* 。

4.  对于 Te.ProcessHost.exe () ，请重复步骤3。

## <a name="diagnose-problems-with-pnp-and-power-management-tests"></a>诊断 PnP 和电源管理测试的问题


可以通过这些命令诊断问题。

[**!powertriage**](../debugger/-powertriage.md) (provides information about system and device power related components) [**!devnode**](../debugger/-devnode.md) (to display information about the PnP tree) [**!process**](../debugger/-process.md) (to examine processes to locate associated threads) [**!thread**](../debugger/-thread.md) (to view information about threads) [**!wdfkd.wdfdevice**](../debugger/-wdfkd-wdfdevice.md) (for WDF driver information) After confirming that there are active PnP or power management threads that are stuck (examine TickCount for this) , follow up with the right component owners.  (您可以找到组件所有者，以查看停滞线程) 的堆栈。

 

