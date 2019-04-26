---
title: 如何分析 IRP 覆盖范围数据
description: 如何分析 IRP 覆盖范围数据
ms.assetid: 71b87948-8e69-4b4a-9546-ea27e96a4bf8
keywords:
- 驱动程序覆盖范围工具包 WDK，分析数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dd6779cd00fb756fccc96f5a057e1eb3ad7110c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63329731"
---
# <a name="how-to-analyze-irp-coverage-data"></a>如何分析 IRP 覆盖范围数据


**请注意**  的驱动程序覆盖范围工具包不再需要在 Windows 10 中，安装程序不再包含在 WDK 中。 若要执行此处所述在 Windows 10 中的任务，请改用[Driver Verifier](driver-verifier.md)并[IRP 日志记录](irp-logging.md)。

 

本主题提供了指导原则来帮助你分析 IRP 覆盖率数据。 有关指南，可帮助你收集 IRP 覆盖率数据，请参阅[如何收集 IRP 覆盖率数据](how-to-collect-irp-coverage-data.md)。

在测试计算机上收集了一个或多个设备的 IRP 覆盖率数据后，可以使用[覆盖率测试 （设备基础）](coverage-tests--device-fundamentals-.md)以生成从这些数据的报表。 这些报表显示单个 I/O 请求数据包 (Irp)，进入或离开指定设备驱动程序堆栈的计数。 未输入或保留驱动程序堆栈的 Irp 的类型也会报告。

对于本主题中，我们使用，例如，从测试计算机上的设备节点 (devnode) 已启用的 IRP 覆盖率数据生成报表。 Devnode 是 9740，和 IRP 覆盖率先前通过运行已对 devnode**启用 IRP 覆盖率数据集合**在测试计算机上的工具。

有关设置 WDK 和 Visual Studio 测试环境的信息，请参阅[方法如何测试在运行时使用 Visual Studio 的驱动程序](https://msdn.microsoft.com/windows-drivers/develop/testing_a_driver_at_runtime)。 有关选择和配置测试和工具参数的信息，请参阅[如何选择和配置设备基础测试](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)并[设备基础测试参数](https://msdn.microsoft.com/windows-drivers/develop/how_to_select_and_configure_the_device_fundamental_tests)。

IRP 覆盖率数据收集后，运行来生成此 devnode IRP 覆盖范围报表**显示收集 IRP 覆盖率数据**在测试计算机上的工具。

```
Drvcov /C 9740
```

IRP 覆盖范围报表具有四个部分：

<span id="Report_Header_______"></span><span id="report_header_______"></span><span id="REPORT_HEADER_______"></span>**报表表头**   
本部分提供有关设备，其 IRP 覆盖率数据显示在报表中的信息。

Devnode 9740 IRP 覆盖范围报表如下所示。

```
Getting coverage data
Data source
 Source Type:  Driver
 Source Name:  \\.\DrvcovControl1
 Device
   Friendly Name : Disk drive 
   Class Name    : DiskDrive 
   Device ID     : IDE\DISKST9320421AS_____________________________SD13____\5&37E07111&0&0.0.0 
   Device #      : 1 
 Devnode #     : 9740
```

<span id="IRP_Major__MJ__and_Minor__MN__Coverage_Data_______"></span><span id="irp_major__mj__and_minor__mn__coverage_data_______"></span><span id="IRP_MAJOR__MJ__AND_MINOR__MN__COVERAGE_DATA_______"></span>**IRP (MJ) 主要和次要的 (MN) 覆盖率数据**   
本部分中显示的计数器 IRP MJ 和其从属 MN IRP 覆盖率期间处理的指定 devnode 的驱动程序的函数代码。 驱动程序覆盖范围工具包监视和报告 52 IRP MJ 和 MJ 函数代码中。

本部分提供有关下列各项的信息：

-   每个 IRP MJ 和 MN 函数代码由驱动程序处理的计数器。 这些计数器可以用于确定哪些 Irp 有足够的测试覆盖率，这可能需要更大的时间。

-   该驱动程序不处理 IRP MJ 和 MN 函数代码的列表。 此信息非常重要，可以帮助您深入了解你的代码覆盖率测试中的缺陷。

**请注意**  有关测试的 Irp 的决策是取决于您的驱动程序和 Irp 驱动程序支持。 IRP MJ 和 MN 覆盖率数据可以帮助您评估您的驱动程序为代码覆盖率测试的效率。

 

Devnode 9740 的 IRP MJ 和 MN 覆盖率数据如以下示例所示：

```
|--------------------------------------------------------|
| MJ & MN Device irp coverage                            |
|--------------------------------------------------------|
| IRPS covered     19                      |  # of times |
|--------------------------------------------------------|
| Unknown                                  |           5 | 
| PNP\QUERY_RESOURCE_REQUIREMENTS          |           3 | 
| PNP\FILTER_RESOURCE_REQUIREMENTS         |           3 | 
| PNP\START_DEVICE                         |           8 | 
| DEVICE_CONTROL                           |         293 | 
| READ                                     |        2543 | 
| PNP\QUERY_CAPABILITIES                   |           3 | 
| PNP\QUERY_PNP_DEVICE_STATE               |           7 | 
| CREATE                                   |          44 | 
| CLEANUP                                  |          45 | 
| CLOSE                                    |          43 | 
| WRITE                                    |        2488 | 
| WMI\REGINFO_EX                           |           5 | 
| WMI\REGINFO                              |           5 | 
| FLUSH_BUFFERS                            |        1491 | 
| PNP\QUERY_DEVICE_RELATIONS\Target        |          23 | 
| WMI\QUERY_ALL_DATA                       |           6 | 
| POWER\QUERY_POWER\SYSTEM                 |           2 | 
| SHUTDOWN                                 |           2 | 
|--------------------------------------------------------|
| IRPS NOT covered     33                  |             |
|--------------------------------------------------------|
| INTERNAL_DEVICE_CONTROL                  |             | 
| POWER\WAIT_WAKE                          |             | 
| POWER\SET_POWER\SYSTEM                   |             | 
| POWER\SET_POWER\DEVICE                   |             | 
| POWER\QUERY_POWER\DEVICE                 |             | 
| WMI\QUERY_SINGLE_INSTANCE                |             | 
| WMI\CHANGE_SINGLE_INSTANCE               |             | 
| WMI\CHANGE_SINGLE_ITEM                   |             | 
| WMI\ENABLE_EVENTS                        |             | 
| WMI\DISABLE_EVENTS                       |             | 
| WMI\ENABLE_COLLECTION                    |             | 
| WMI\DISABLE_COLLECTION                   |             | 
| WMI\EXECUTE_METHOD                       |             | 
| PNP\QUERY_REMOVE_DEVICE                  |             | 
| PNP\REMOVE_DEVICE                        |             | 
| PNP\CANCEL_REMOVE_DEVICE                 |             | 
| PNP\STOP_DEVICE                          |             | 
| PNP\QUERY_STOP_DEVICE                    |             | 
| PNP\CANCEL_STOP_DEVICE                   |             | 
| PNP\QUERY_DEVICE_RELATIONS\Bus           |             | 
| PNP\QUERY_DEVICE_RELATIONS\Eject         |             | 
| PNP\QUERY_DEVICE_RELATIONS\Removal       |             | 
| PNP\QUERY_INTERFACE                      |             | 
| PNP\QUERY_RESOURCES                      |             | 
| PNP\QUERY_DEVICE_TEXT                    |             | 
| PNP\READ_CONFIG                          |             | 
| PNP\WRITE_CONFIG                         |             | 
| PNP\EJECT                                |             | 
| PNP\SET_LOCK                             |             | 
| PNP\QUERY_ID                             |             | 
| PNP\QUERY_BUS_INFORMATION                |             | 
| PNP\DEVICE_USAGE_NOTIFICATION            |             | 
| PNP\SURPRISE_REMOVAL                     |             | 
|--------------------------------------------------------|
| Stats                                                  |
|--------------------------------------------------------|
| Total IRP count        :     52                        |
| Covered IRP count      :     19                        |
| NOT Covered IRP count  :     33                        |
| Covered IRP %          :     36.54%                    |
| NOT Covered IRP %      :     63.46%                    |
|--------------------------------------------------------|
```

<span id="IRP_MJ_Coverage_Data_______"></span><span id="irp_mj_coverage_data_______"></span><span id="IRP_MJ_COVERAGE_DATA_______"></span>**IRP MJ 覆盖率数据**   
本部分显示了仅 IRP MJ IRP 覆盖率期间处理的指定 devnode 的驱动程序的函数代码的计数器。 驱动程序覆盖范围工具包监视和报告 13 IRP MJ 函数代码中。

本部分提供有关下列各项的信息：

-   驱动程序处理每个 IRP MJ 函数代码的计数器。 可以使用这些计数器来确定哪些 Irp 有足够的测试覆盖率，这可能需要更大的时间。

-   该驱动程序不处理 IRP MJ 函数代码的列表。 此信息非常重要，可以帮助您深入了解你的代码覆盖率测试中的缺陷。

作为使用 IRP MJ 和 MN 覆盖率数据，在本部分中的数据可以用于分析代码覆盖率测试的效率。 具体而言，此数据显示为每个 IRP MJ 函数代码的驱动程序的调度例程程度进行了测试。

Devnode 9740 的 IRP MJ 覆盖率数据如以下示例所示：

```
|--------------------------------------------------------|
| MJ Device irp coverage                                 |
|--------------------------------------------------------|
| IRPS covered     12                      |  # of times |
|--------------------------------------------------------|
| IRP_MJ_UNKNOWN                           |           1 | 
| IRP_MJ_PNP                               |           6 | 
| IRP_MJ_DEVICE_CONTROL                    |           1 | 
| IRP_MJ_READ                              |           1 | 
| IRP_MJ_CREATE                            |           1 | 
| IRP_MJ_CLEANUP                           |           1 | 
| IRP_MJ_CLOSE                             |           1 | 
| IRP_MJ_WRITE                             |           1 | 
| IRP_MJ_SYSTEM_CONTROL                    |           3 | 
| IRP_MJ_FLUSH_BUFFERS                     |           1 | 
| IRP_MJ_POWER                             |           1 | 
| IRP_MJ_SHUTDOWN                          |           1 | 
|--------------------------------------------------------|
| IRPS NOT covered      1                  |             |
|--------------------------------------------------------|
| IRP_MJ_INTERNAL_DEVICE_CONTROL           |             | 
|--------------------------------------------------------|
| Stats                                                  |
|--------------------------------------------------------|
| Total IRP count        :     13                        |
| Covered IRP count      :     12                        |
| NOT Covered IRP count  :      1                        |
| Covered IRP %          :     92.31%                    |
| NOT Covered IRP %      :      7.69%                    |
|--------------------------------------------------------|
```

<span id="IRP_Pairs_Coverage_Data_______"></span><span id="irp_pairs_coverage_data_______"></span><span id="IRP_PAIRS_COVERAGE_DATA_______"></span>**IRP 对覆盖率数据**   
本部分介绍的 Irp 一对期间 devnode 的驱动程序堆栈中并发活动 IRP 覆盖范围内的次数。 驱动程序覆盖范围工具包监视和报告上 1099年不同 IRP 对。

本部分中的每个 IRP MJ MJ/MN 函数代码同时处理由驱动程序的显示的计数器。 这些计数器可以用于确定哪些 Irp 有足够的测试覆盖率，这可能需要更大的时间。

为与其他类型的 IRP 覆盖率数据，在本部分中的数据可以用于分析代码覆盖率测试的效率。 但是，此数据很大不同的因为它揭示了如何驱动程序进行了测试并发 IRP 处理。

Devnode 9740 的 IRP 对覆盖率数据如以下示例所示：

```
|--------------------------------------------------------|
| MJ & MN Device IRP Concurrency pairs.                  |
|--------------------------------------------------------|
| IRP Pairs covered                     25 |  # of times |
|--------------------------------------------------------|
| CREATE                                   |             | 
| READ                                     |          10 | 
|--------------------------------------------------------|
| CREATE                                   |             | 
| WRITE                                    |           5 | 
|--------------------------------------------------------|
| CREATE                                   |             | 
| DEVICE_CONTROL                           |           4 | 
|--------------------------------------------------------|
| CLOSE                                    |             | 
| READ                                     |          10 | 
|--------------------------------------------------------|
| CLOSE                                    |             | 
| WRITE                                    |           4 | 
|--------------------------------------------------------|
| CLOSE                                    |             | 
| DEVICE_CONTROL                           |           4 | 
|--------------------------------------------------------|
| READ                                     |             | 
| READ                                     |        1513 | 
|--------------------------------------------------------|
| READ                                     |             | 
| WRITE                                    |        1498 | 
|--------------------------------------------------------|
| READ                                     |             | 
| FLUSH_BUFFERS                            |         929 | 
|--------------------------------------------------------|
| READ                                     |             | 
| DEVICE_CONTROL                           |          68 | 
|--------------------------------------------------------|
| READ                                     |             | 
| CLEANUP                                  |          11 | 
|--------------------------------------------------------|
| READ                                     |             | 
| POWER\QUERY_POWER\SYSTEM                 |           1 | 
|--------------------------------------------------------|
| READ                                     |             | 
| WMI\QUERY_ALL_DATA                       |           2 | 
|--------------------------------------------------------|
| READ                                     |             | 
| PNP\QUERY_DEVICE_RELATIONS\Target        |           7 | 
|--------------------------------------------------------|
| READ                                     |             | 
| PNP\QUERY_PNP_DEVICE_STATE               |           1 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| WRITE                                    |        1448 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| FLUSH_BUFFERS                            |         852 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| DEVICE_CONTROL                           |           8 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| CLEANUP                                  |           4 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| PNP\QUERY_DEVICE_RELATIONS\Target        |           1 | 
|--------------------------------------------------------|
| WRITE                                    |             | 
| PNP\QUERY_PNP_DEVICE_STATE               |           2 | 
|--------------------------------------------------------|
| FLUSH_BUFFERS                            |             | 
| FLUSH_BUFFERS                            |          27 | 
|--------------------------------------------------------|
| FLUSH_BUFFERS                            |             | 
| DEVICE_CONTROL                           |           1 | 
|--------------------------------------------------------|
| DEVICE_CONTROL                           |             | 
| CLEANUP                                  |           7 | 
|--------------------------------------------------------|
| DEVICE_CONTROL                           |             | 
| PNP\START_DEVICE                         |           2 | 
|--------------------------------------------------------|
|--------------------------------------------------------|
| Stats                                                  |
|--------------------------------------------------------|
| Total IRP pairs                 :        1099          |
| Covered IRP pairs               :          25          |
| NOT Covered IRP pairs           :        1074          |
| Covered IRP pairs %             :           2.27%      |
| NOT Covered IRP pairs %         :          97.73%      |
|--------------------------------------------------------|
```

 

 





