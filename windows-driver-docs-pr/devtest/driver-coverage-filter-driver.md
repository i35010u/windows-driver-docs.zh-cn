---
title: 驱动程序覆盖范围筛选器驱动程序
description: 驱动程序覆盖范围筛选器驱动程序
keywords:
- 驱动程序覆盖套件 WDK，筛选器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c213778a36ca5c2a642a41a24c57d135e404234a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839011"
---
# <a name="driver-coverage-filter-driver"></a>驱动程序覆盖范围筛选器驱动程序


**注意**  Windows 10 不再需要驱动程序覆盖率工具包，并且 WDK 中不再包括该安装程序。 若要在 Windows 10 中执行此处所述的任务，请改用 [驱动程序验证程序](driver-verifier.md) 和 [IRP 日志记录](irp-logging.md)。

 

 ( # A0) 的驱动程序覆盖率筛选器驱动程序监视 (Irp) 输入或保留指定设备的驱动程序堆栈的 i/o 请求数据包。 在运行 "**启用 IRP 覆盖率" 数据收集** 工具时，通过使用 *DQ* 参数指定驱动程序覆盖率筛选器驱动程序监视的设备。 请参阅 [如何选择和配置设备基础测试](/windows-hardware/drivers) 和 [设备基础测试参数](/windows-hardware/drivers)。

<span id="UpperFilter___TRUE"></span><span id="upperfilter___true"></span><span id="UPPERFILTER___TRUE"></span>**UpperFilter = TRUE**  
此选项将驱动程序覆盖率筛选器驱动程序安装为指定设备的设备驱动程序的上限筛选器。 此配置监视设备驱动程序堆栈中的设备驱动程序的所有 IRP 流量，无论驱动程序是处理 IRP 还是传递到更低的设备驱动程序。

<span id="UpperFilter___FALSE"></span><span id="upperfilter___false"></span><span id="UPPERFILTER___FALSE"></span>**UpperFilter = FALSE**  
此选项将驱动程序覆盖率筛选器驱动程序安装为指定设备的设备驱动程序的较低筛选器。 此配置监视设备驱动程序堆栈中较低驱动程序的设备驱动程序的所有 IRP 流量。

下图显示了驱动程序覆盖率筛选器驱动程序作为上层筛选器安装的设备的 "驱动程序堆栈" 和 "IRP 监视" 窗口。 在此配置中，筛选器驱动程序跟踪为指定设备进入或离开驱动程序的所有 Irp。

![说明安装为上限筛选器的驱动程序覆盖率筛选器驱动程序的关系图](images/coverage-1.png)

下图显示了一个设备的驱动程序堆栈和 IRP 监视窗口，其中，驱动程序覆盖率筛选器驱动程序安装为较低的筛选器。 在此配置中，筛选器驱动程序跟踪为指定设备的驱动程序堆栈进入或离开设备驱动程序的所有 Irp。

![说明驱动程序覆盖率筛选器驱动程序安装为较低筛选器的关系图](images/coverage-2.png)

.

### <a name="span-idinstalling_the_driver_coverage_filter_driverspanspan-idinstalling_the_driver_coverage_filter_driverspan-installing-the-driver-coverage-filter-driver"></a><span id="installing_the_driver_coverage_filter_driver"></span><span id="INSTALLING_THE_DRIVER_COVERAGE_FILTER_DRIVER"></span> 安装驱动程序覆盖率筛选器驱动程序

以下规则定义了安装驱动程序覆盖率筛选器驱动程序以监视 Irp 的最佳方式：

-   如果希望在特定设备和用户模式应用程序或服务之间进行 IRP 流量，请将筛选器驱动程序安装为设备驱动程序的筛选器。

-   如果要在指定的设备和驱动程序堆栈中的设备（例如设备的总线驱动程序）之间 IRP 流量，请将筛选器驱动程序安装为设备驱动程序的较低筛选器。

**注意**   如何安装驱动程序覆盖率筛选器驱动程序以获得最佳 IRP 覆盖范围取决于驱动程序堆栈的拓扑，并要求您了解堆栈内驱动程序的关系和顺序。

 

 

