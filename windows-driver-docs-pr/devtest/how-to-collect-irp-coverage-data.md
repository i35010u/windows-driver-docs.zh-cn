---
title: 如何收集 IRP 覆盖范围数据
description: 如何收集 IRP 覆盖范围数据
keywords:
- 驱动程序覆盖套件 WDK，收集数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63d7e2a3dd5f0f091bda7820ed7f7f1120797144
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803585"
---
# <a name="how-to-collect-irp-coverage-data"></a>如何收集 IRP 覆盖范围数据


**注意**  Windows 10 不再需要驱动程序覆盖率工具包，并且 WDK 中不再包括该安装程序。 若要在 Windows 10 中执行此处所述的任务，请改用 [驱动程序验证程序](driver-verifier.md) 和 [IRP 日志记录](irp-logging.md)。

 

以下步骤介绍如何使用驱动程序覆盖率工具和 [驱动程序覆盖率筛选器驱动](driver-coverage-filter-driver.md)程序，收集 (irp) 的 i/o 请求包的覆盖率数据。 该工具可作为 [设备基础测试](device-fundamentals-tests.md)的一部分，在 "覆盖率" 类别下。

有关设置 WDK 和 Visual Studio 测试环境的信息，请参阅 [如何使用 Visual studio 在运行时测试驱动程序](/windows-hardware/drivers)。 有关选择和配置测试和工具参数的信息，请参阅 [如何选择和配置设备基础测试](/windows-hardware/drivers) 和 [设备基础测试参数](/windows-hardware/drivers)。

1.  在测试计算机上安装 [驱动程序覆盖率筛选器驱动程序](driver-coverage-filter-driver.md) 。

    -   若要在指定的设备上安装筛选器驱动程序并启用 IRP 覆盖 () ，请运行 **启用 IRP 覆盖率数据收集** 工具。 在覆盖范围内，该工具作为 [设备基础测试](device-fundamentals-tests.md)的一部分提供。

    -   若要在) 的指定设备上安装筛选器驱动程序并启用 IRP 覆盖，请使用 *DQ* 参数指定要监视的设备)  ( (。

    -   若要安装驱动程序覆盖率筛选器驱动程序作为筛选器驱动程序的筛选器驱动程序或较低筛选器驱动 (程序，) 使用 *UpperFilter* 参数。 有关覆盖率筛选器驱动程序的信息以及有关如何安装驱动程序的指南，请参阅 [驱动程序覆盖率筛选器驱动程序](driver-coverage-filter-driver.md)

    有关运行这些工具的信息，请参阅 [如何使用 Visual Studio 在运行时测试驱动程序](/windows-hardware/drivers) 以及 [如何选择和配置设备基础测试](/windows-hardware/drivers)。

2.  清除当前的 IRP 覆盖率数据。

    在一个或多个设备上开始你的代码覆盖率测试之前，请先清除已由 [驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)收集的 IRP 覆盖率数据。 为此，请在测试计算机上运行 " **清除 IRP 覆盖率数据** " 工具。

3.  重新启动测试计算机。

    在一个或多个设备上安装 [驱动程序覆盖面筛选器驱动程序](driver-coverage-filter-driver.md) 后，请重新启动测试计算机以加载驱动程序覆盖率筛选器驱动程序并启动 IRP 覆盖范围。

4.  验证是否安装了 [驱动程序覆盖率筛选器驱动程序](driver-coverage-filter-driver.md) 。

    重新启动测试计算机后，验证是否安装了筛选器驱动程序，并为 IRP 覆盖装置启用了正确的设备。 为此，请在测试计算机上运行 **为 IRP 覆盖率数据收集工具启用的 "显示设备** "。

    ```
    Drvcov /D
    ```

    下面的示例显示了此工具的示例输出：

    ```
    |------------------------------------------------------------------
    | List of devices we can get coverage data from.
    |------------------------------------------------------------------
    |  Device # : 1 
    |  Devnode #: 3884 Class:  USB Desc:  USB Root Hub
    |  Device ID: " USB\ROOT_HUB\4&413399C&0"
    |------------------------------------------------------------------
    | 1 device(s) found.
    |------------------------------------------------------------------
    ```

5.  收集 IRP 覆盖率数据。

    你现在可以为设备 () 收集 IRP 覆盖率数据。 首先在测试计算机上运行代码覆盖率测试。 运行完代码覆盖率测试后，可以查看 IRP 覆盖率报告。 为此，请在测试计算机上运行 **显示收集的 IRP 覆盖率数据** 工具。

    有关如何分析 IRP 覆盖率数据的信息，请参阅 [如何分析 Irp 覆盖率数据](how-to-analyze-irp-coverage-data.md)。

6.  禁用 IRP 覆盖范围并卸载 [驱动程序覆盖率筛选器驱动程序](driver-coverage-filter-driver.md)。

    完全执行代码覆盖率测试后，可以通过在测试计算机上运行 " **禁用 irp 覆盖率数据收集** " 工具，禁用 irp 覆盖所有设备。

    如果为 IRP 覆盖装置禁用了最后一个设备，则每次重新启动测试计算机时，筛选器驱动程序将不再加载。 但是，若要从内存中卸载筛选器驱动程序，则必须重新启动测试计算机。

 

