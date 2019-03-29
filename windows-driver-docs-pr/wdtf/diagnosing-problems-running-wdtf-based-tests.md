---
title: 对运行基于 WDTF 的测试时出现的问题进行诊断
description: 若要帮助您解决运行 WDTF 基于测试的问题，可以使用调试程序。
ms.assetid: 24257B50-ED9C-4D45-A245-1EC855463D33
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5136738c5fb9a69b6508ee3bafab18ba23616a03
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566302"
---
# <a name="diagnosing-problems-running-wdtf-based-tests"></a>对运行基于 WDTF 的测试时出现的问题进行诊断


若要帮助您解决运行 WDTF 基于测试的问题，可以使用调试程序。

## <a name="diagnose-problems-with-unresponsive-wdtf-based-tests-run-from-visual-studio"></a>诊断响应基于 WDTF 的测试 （Visual Studio 中运行） 的问题


1.  配置并连接到正在运行基于 WDTF 的测试的计算机的内核调试程序。 请参阅[预配计算机，以使驱动程序部署和测试 (WDK 8.1)](https://msdn.microsoft.com/library/windows/hardware/dn745909)或[预配计算机，以使驱动程序部署和测试 (WDK 8)](https://msdn.microsoft.com/library/windows/hardware/dn745909)。
2.  搜索 Te.exe 进程和切换到该进程的上下文。 Te.exe 有关的信息，请参阅[测试创作和执行框架 (TAEF)](https://msdn.microsoft.com/library/windows/hardware/hh439725)。

    ``` syntax
    !process 0 0 Te.exe 

    PROCESS fffffa80093c6340

    SessionId: 1 Cid: 1320 Peb: 7f6595b3000 ParentCid: 12a0

    DirBase: 21eee000 ObjectTable: fffff8a0035b0a00 HandleCount: 327.

    Image: TE.exe

    ·         .process /p /r fffffa80093c6340

    ·         
    ```

3.  运行[ **！ 过程**](https://msdn.microsoft.com/library/windows/hardware/ff564717)命令标识 Te.exe 下运行的线程。

    ``` syntax
    !process fffffa80093c6340
    ```

    查找与线程**WDTF** \*在堆栈上。

4.  （如果存在） 为 Te.ProcessHost.exe 重复步骤 3。

## <a name="diagnose-problems-with-pnp-and-power-management-tests"></a>诊断问题的即插即用和电源管理测试


您可以诊断问题使用以下命令。

[**！ powertriage** ](https://msdn.microsoft.com/library/windows/hardware/mt431710) （提供有关系统和设备电源相关的组件的信息） [ **！ devnode** ](https://msdn.microsoft.com/library/windows/hardware/ff562345) （若要显示的即插即用的树有关的信息） [**！ 过程**](https://msdn.microsoft.com/library/windows/hardware/ff564717) （若要检查进程来查找关联的线程） [ **！ 线程**](https://msdn.microsoft.com/library/windows/hardware/ff565440) （若要查看有关线程的信息） [ **！ wdfkd.wdfdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff565703) （有关 WDF 驱动程序信息） 确认有活动的即插即用或电源管理线程之后 （检查此 TickCount），请使用正确的组件所有者的财产。 （可以找到从查看卡滞线程的堆栈组件所有者）。

 

 




