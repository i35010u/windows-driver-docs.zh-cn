---
title: 驱动程序覆盖范围筛选器驱动程序
description: 驱动程序覆盖范围筛选器驱动程序
ms.assetid: 8d345081-b9be-4e22-9276-dacd7815f506
keywords:
- 驱动程序覆盖范围工具包 WDK，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca9df66e8e272b8cafa1af70ec182d0462e6a42
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542119"
---
# <a name="driver-coverage-filter-driver"></a>驱动程序覆盖范围筛选器驱动程序


**请注意**  的驱动程序覆盖范围工具包不再需要在 Windows 10 中，安装程序不再包含在 WDK 中。 若要执行此处所述在 Windows 10 中的任务，请改用[Driver Verifier](driver-verifier.md)并[IRP 日志记录](irp-logging.md)。

 

驱动程序覆盖范围筛选器驱动程序 (Drvcov.sys) 监视 I/O 请求数据包 (Irp)，进入或离开指定设备驱动程序堆栈。 指定的设备的驱动程序覆盖范围筛选器驱动程序将使用监视*DQ*参数运行时**启用 IRP 覆盖率数据集合**工具。 请参阅[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)并[设备基础测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)。

<span id="UpperFilter___TRUE"></span><span id="upperfilter___true"></span><span id="UPPERFILTER___TRUE"></span>**UpperFilter = TRUE**  
此选项将安装为上部设备驱动程序筛选器指定设备驱动程序覆盖范围筛选器驱动程序。 此配置监视所有 IRP 流量传入或传出设备的驱动程序堆栈，无论该驱动程序处理 IRP 还是通过其传递到较低的设备驱动程序中的设备驱动程序。

<span id="UpperFilter___FALSE"></span><span id="upperfilter___false"></span><span id="UPPERFILTER___FALSE"></span>**UpperFilter = FALSE**  
此选项将安装为较低的设备驱动程序筛选器指定设备驱动程序覆盖范围筛选器驱动程序。 此配置监视所有 IRP 流量传入或传出中设备的驱动程序堆栈的低级驱动程序中的设备驱动程序。

下图显示了驱动程序堆栈和 IRP 监视窗口的设备驱动程序覆盖范围筛选器驱动程序为上限的筛选器的安装。 在此配置中，筛选器驱动程序跟踪所有 Irp，进入或离开指定设备的驱动程序。

![说明为上限的筛选器安装了驱动程序覆盖范围筛选器驱动程序的关系图](images/coverage-1.png)

下图显示了驱动程序堆栈和 IRP 监视窗口中的设备驱动程序覆盖范围筛选器驱动程序为较低的筛选器的安装。 在此配置中，筛选器驱动程序跟踪所有 Irp，进入或离开指定的设备驱动程序堆栈的设备驱动程序。

![说明为较低的筛选器安装了驱动程序覆盖范围筛选器驱动程序的关系图](images/coverage-2.png)

.

### <a name="span-idinstallingthedrivercoveragefilterdriverspanspan-idinstallingthedrivercoveragefilterdriverspan-installing-the-driver-coverage-filter-driver"></a><span id="installing_the_driver_coverage_filter_driver"></span><span id="INSTALLING_THE_DRIVER_COVERAGE_FILTER_DRIVER"></span> 安装驱动程序覆盖范围筛选器驱动程序

以下规则定义安装驱动程序覆盖范围筛选器驱动程序来监视 Irp 的最佳方法：

-   如果您希望为特定设备和用户模式应用程序或服务之间的 IRP 流量的覆盖率数据，作为设备驱动程序的上部筛选器安装筛选器驱动程序。

-   如果您希望覆盖率数据 IRP 之间的通信指定的设备和设备驱动程序堆栈，例如设备的总线驱动程序中较低级别安装筛选器驱动程序作为设备驱动程序的较低筛选器。

**请注意**  如何安装驱动程序覆盖范围筛选器驱动程序，获得最佳的 IRP 覆盖范围取决于驱动程序堆栈的拓扑，并要求您了解的关系和堆栈内的驱动程序的顺序。

 

 

 





