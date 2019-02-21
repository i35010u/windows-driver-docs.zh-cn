---
title: 如何收集 IRP 覆盖率数据
description: 如何收集 IRP 覆盖率数据
ms.assetid: f65422fe-f524-41c1-a532-a2c615d65f72
keywords:
- 驱动程序覆盖范围工具包 WDK，收集数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8dc6b124c4f2389398b2dfca040ff249b30288cd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545450"
---
# <a name="how-to-collect-irp-coverage-data"></a>如何收集 IRP 覆盖率数据


**请注意**  的驱动程序覆盖范围工具包不再需要在 Windows 10 中，安装程序不再包含在 WDK 中。 若要执行此处所述在 Windows 10 中的任务，请改用[Driver Verifier](driver-verifier.md)并[IRP 日志记录](irp-logging.md)。

 

以下步骤介绍如何使用驱动程序覆盖范围工具收集覆盖率数据的 I/O 请求数据包 (Irp) 和[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)。 工具是可作为的一部分[设备基础测试](device-fundamentals-tests.md)，覆盖率类别下。

有关设置 WDK 和 Visual Studio 测试环境的信息，请参阅[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)。 有关选择和配置测试和工具参数的信息，请参阅[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)并[设备基础测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)。

1.  安装[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)在测试计算机上。

    -   若要安装的筛选器驱动程序和启用指定设备上的 IRP 覆盖率，请运行**启用 IRP 覆盖率数据集合**工具。 该工具是可作为的一部分[设备基础测试](device-fundamentals-tests.md)，覆盖率下。

    -   若要安装筛选器驱动程序和启用指定设备上的 IRP 覆盖率，请使用*DQ*参数来指定要监视的设备。

    -   若要安装驱动程序覆盖范围筛选器驱动程序作为上限筛选器驱动程序或更低筛选器驱动程序设备使用*UpperFilter*参数。 覆盖率筛选器驱动程序有关的信息和有关如何安装驱动程序的指南，请参阅[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)

    运行工具的信息，请参阅[如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)并[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)。

2.  清除当前的 IRP 覆盖率数据。

    一个或多个设备上启动代码覆盖率测试之前，请首先清除已收集的 IRP 覆盖率数据[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)。 若要执行此操作，请运行**清除 IRP 覆盖率数据**在测试计算机上的工具。

3.  重新启动测试计算机。

    安装后[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)在一个或多个设备上重新启动测试计算机以加载驱动程序覆盖范围筛选器驱动程序和启动 IRP 覆盖率。

4.  验证是否[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)安装。

    测试完成后重新启动计算机，请验证筛选器驱动程序已安装正确的设备启用了 IRP 覆盖率。 若要执行此操作，请运行**IRP 覆盖率数据收集已启用的显示设备**在测试计算机上的工具。

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

    现在你可以在设备的 IRP 覆盖率数据收集。 首先在测试计算机上运行代码覆盖率测试。 完成运行代码覆盖率测试后，可以查看 IRP 覆盖率报表。 若要执行此操作，请运行**显示收集 IRP 覆盖率数据**在测试计算机上的工具。

    有关如何分析 IRP 覆盖率数据的信息，请参阅[如何分析 IRP 覆盖率数据](how-to-analyze-irp-coverage-data.md)。

6.  禁用 IRP 覆盖和卸载[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)。

    您完全执行代码覆盖率测试后，您可以禁用 IRP 覆盖所有设备通过运行**都禁用 IRP 覆盖率数据集合**在测试计算机上的工具。

    在最后一台设备已被禁用的 IRP 覆盖率，每当重新启动测试计算机都将不再加载筛选器驱动程序。 但是，若要卸载内存中的筛选器驱动程序，您必须重新启动测试计算机。

 

 





