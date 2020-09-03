---
title: 如何分析 IRP 覆盖范围数据
description: 如何分析 IRP 覆盖范围数据
ms.assetid: 71b87948-8e69-4b4a-9546-ea27e96a4bf8
keywords:
- 驱动程序覆盖套件 WDK，分析数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7d089029e2383160a14164e01c82215a7453d80
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384837"
---
# <a name="how-to-analyze-irp-coverage-data"></a>如何分析 IRP 覆盖范围数据


**注意**   Windows 10 不再需要驱动程序覆盖率工具包，并且 WDK 中不再包括该安装程序。 若要在 Windows 10 中执行此处所述的任务，请改用 [驱动程序验证程序](driver-verifier.md) 和 [IRP 日志记录](irp-logging.md)。

 

本主题提供帮助你分析 IRP 覆盖率数据的指南。 有关帮助您收集 IRP 覆盖率数据的指南，请参阅 [如何收集 Irp 覆盖率数据](how-to-collect-irp-coverage-data.md)。

收集测试计算机上的一个或多个设备的 IRP 覆盖率数据后，可以使用 [ (设备基础) 的覆盖率测试 ](coverage-tests--device-fundamentals-.md) ，从此数据生成报表。 这些报告显示为指定设备输入或离开驱动程序堆栈 (Irp) 的单个 i/o 请求数据包的计数。 还会报告未进入或离开驱动程序堆栈的 Irp 类型。

对于本主题，我们将使用，作为一个示例，我们使用为设备节点启用的 IRP 覆盖面数据（ (devnode) 在测试计算机上）生成的报表。 Devnode 为9740，并且已通过在测试计算机上运行 " **启用 irp 覆盖率" 数据收集** 工具为 devnode 启用了 irp 覆盖区。

有关设置 WDK 和 Visual Studio 测试环境的信息，请参阅 [如何使用 Visual studio 在运行时测试驱动程序](/windows-hardware/drivers)。 有关选择和配置测试和工具参数的信息，请参阅 [如何选择和配置设备基础测试](/windows-hardware/drivers) 和 [设备基础测试参数](/windows-hardware/drivers)。

收集 IRP 覆盖率数据后，将通过在测试计算机上运行 " **显示收集的 IRP 覆盖率数据** " 工具来生成此 DEVNODE 的 irp 覆盖范围报告。

```
Drvcov /C 9740
```

IRP 覆盖范围报表包含四个部分：

<span id="Report_Header_______"></span><span id="report_header_______"></span><span id="REPORT_HEADER_______"></span>**报表表头**   
本部分提供有关设备的信息，其 IRP 覆盖率数据显示在报表中。

Devnode 9740 的 IRP 覆盖率报表如下所示。

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

<span id="IRP_Major__MJ__and_Minor__MN__Coverage_Data_______"></span><span id="irp_major__mj__and_minor__mn__coverage_data_______"></span><span id="IRP_MAJOR__MJ__AND_MINOR__MN__COVERAGE_DATA_______"></span>**IRP 主 (MJ) 和次要 (MN) 覆盖率数据**   
本部分说明 irp MJ 的计数器，以及在 IRP 范围内由指定的 devnode 的驱动程序处理的子 MN 函数代码的计数器。 驱动程序覆盖率工具包监视和报告 52 IRP MJ 和 MJ 函数代码。

本节提供有关以下方面的信息：

-   驱动程序处理的每个 IRP MJ 和 MN 函数代码的计数器。 这些计数器可用于确定哪些 Irp 具有足够的测试覆盖率，哪些 Irp 可能需要更多的范围。

-   驱动程序未处理的 IRP MJ 和 MN 函数代码的列表。 此信息非常重要，可提供有关代码覆盖率测试中的缺陷的见解。

**注意**   关于要测试哪个 Irp 的决策取决于驱动程序和驱动程序支持的 Irp。 IRP MJ 和 MN 覆盖率数据可帮助你评估你的驱动程序的代码覆盖率测试的效率。

 

Devnode 9740 的 IRP MJ 和 MN 覆盖率数据显示在以下示例中：

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
此部分仅显示 irp 范围内由指定 devnode 的驱动程序处理的 IRP MJ 函数代码的计数器。 驱动程序覆盖率工具包监视和报告 13 IRP MJ 函数代码。

本节提供有关以下方面的信息：

-   驱动程序处理的每个 IRP MJ 函数代码的计数器。 您可以使用这些计数器来确定哪些 Irp 具有足够的测试覆盖率，哪些 Irp 可能需要更多的范围。

-   驱动程序未处理的 IRP MJ 函数代码的列表。 此信息非常重要，可提供有关代码覆盖率测试中的缺陷的见解。

对于 IRP MJ 和 MN 覆盖率数据，本节中的数据可用于分析代码覆盖率测试的效率。 具体而言，此数据显示测试的每个 IRP MJ 函数代码的驱动程序调度例程的程度。

Devnode 9740 的 IRP MJ 覆盖率数据显示在以下示例中：

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
此部分显示 IRP 范围内一对 Irp 在 devnode 的驱动程序堆栈内并发活动的次数。 驱动程序覆盖率工具包监视和报告1099不同的 IRP 对。

此部分显示了驱动程序并发处理的 MJ/MN 函数代码的每个 IRP MJ 的计数器。 这些计数器可用于确定哪些 Irp 具有足够的测试覆盖率，哪些 Irp 可能需要更多的范围。

与其他类型的 IRP 覆盖率数据一样，本节中的数据可用于分析代码覆盖率测试的效率。 但是，此数据明显不同，因为它显示了驱动程序在并发 IRP 处理中的测试情况。

Devnode 9740 的 IRP 对覆盖率数据显示在以下示例中：

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

 

