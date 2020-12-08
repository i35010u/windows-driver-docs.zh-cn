---
title: 驱动程序覆盖范围工具包概述
description: 驱动程序覆盖范围工具包概述
keywords:
- 驱动程序覆盖套件 WDK，关于驱动程序覆盖套件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 40a491c2324b630ef0c3715c93670eb7db3718c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784025"
---
# <a name="overview-of-the-driver-coverage-toolkit"></a>驱动程序覆盖范围工具包概述


**注意**  Windows 10 不再需要驱动程序覆盖率工具包，并且 WDK 中不再包括该安装程序。 若要在 Windows 10 中执行此处所述的任务，请改用 [驱动程序验证程序](driver-verifier.md) 和 [IRP 日志记录](irp-logging.md)。

 

驱动程序范围工具包监视和报告 i/o 请求数据包 (Irp) 为一个或多个指定设备进入或离开驱动程序堆栈。 这些设备的 [驱动程序覆盖率筛选器驱动程序](driver-coverage-filter-driver.md) 收集覆盖率数据。 驱动程序覆盖工具用于在指定的设备上启用或禁用 IRP 覆盖区，并从覆盖面数据生成报表。

驱动程序覆盖套件根据以下三个指标收集和报告 IRP 覆盖率数据：

<span id="Major__MJ__IRP_Function_Codes"></span><span id="major__mj__irp_function_codes"></span><span id="MAJOR__MJ__IRP_FUNCTION_CODES"></span>主 (MJ) IRP 函数代码  
设备的驱动程序堆栈内处于活动状态的 Irp 的 MJ 函数代码计数。 驱动程序覆盖率工具包收集12个 MJ 函数代码的数据。 有关这些函数代码的详细信息，请参阅 [IRP 主要功能代码](../kernel/irp-major-function-codes.md)。

<span id="Major__MJ__and_Minor__MN__IRP_Function_Codes"></span><span id="major__mj__and_minor__mn__irp_function_codes"></span><span id="MAJOR__MJ__AND_MINOR__MN__IRP_FUNCTION_CODES"></span>主 (MJ) 和次要 (MN) IRP 函数代码  
在设备的驱动程序堆栈内处于活动状态的 Irp 的 MJ IRP 函数代码及其从属 MN 函数代码的计数。 驱动程序覆盖率工具包收集 52 MJ 和 MN 函数代码的数据。

<span id="IRP_Pairs"></span><span id="irp_pairs"></span><span id="IRP_PAIRS"></span>IRP 对  
在设备的驱动程序堆栈内并发活动的 MJ 和 MJ/MN IRP 函数代码的计数。 此计数反映了在同一时间进入或离开驱动程序堆栈的单独 Irp 的次数。 驱动程序覆盖率工具包收集 1099 MJ 和 MN 函数代码对的数据。

有关 IRP 函数代码的详细信息，请参阅 [Irp 函数代码](/previous-versions/windows/hardware/drivers/ff550706(v=vs.85))。

### <a name="span-idirp_coverage_dataspanspan-idirp_coverage_dataspanirp-coverage-data"></a><span id="irp_coverage_data"></span><span id="IRP_COVERAGE_DATA"></span>IRP 覆盖率数据

无论何时为 [驱动程序覆盖面筛选器驱动程序](driver-coverage-filter-driver.md)监视的设备进入或离开驱动程序堆栈，筛选器驱动程序都将增加与 IRP 相关的计数器。 驱动程序覆盖率筛选器驱动程序监视驱动程序堆栈中的活动 Irp，而不管 Irp 是如何产生的。 因此，筛选器驱动程序的 IRP 的 "监视" 窗口会涵盖堆栈中紧靠筛选器驱动程序下的所有驱动程序。

[驱动程序覆盖率筛选器驱动](driver-coverage-filter-driver.md)程序在首次监视驱动程序堆栈中的 irp 时，会递增其 irp 计数器。 如果 IRP 源自驱动程序堆栈，则驱动程序覆盖率筛选器驱动程序会在 IRP 输入堆栈时为 IRP 增加其计数器。 如果 IRP 源自驱动程序堆栈中的驱动程序，则当 IRP 离开驱动程序堆栈时，筛选器驱动程序会递增其计数器。

下图显示了设备的驱动程序堆栈内的 IRP 流量的示例。

![说明设备的驱动程序堆栈中的 i/o 请求数据包 (irp) 流量的关系图](images/coverage-3.png)

在此示例中， [驱动程序覆盖率筛选器驱动程序](driver-coverage-filter-driver.md) 监视以下 irp：

-   IRP A，它刚刚进入了驱动程序堆栈。

-   IRP B，它即将离开驱动程序堆栈。

驱动程序覆盖率筛选器驱动程序为两个 Irp 递增其 MN 和 MN/MJ 函数代码计数器。 此外，由于在驱动程序堆栈内两个 Irp A 和 B 都处于活动状态，因此驱动程序覆盖率筛选器驱动程序会递增该元组 {IRP A，IRP B} 的 IRP 对计数器的值。

### <a name="span-idirp_pair_coverage_dataspanspan-idirp_pair_coverage_dataspanirp-pair-coverage-data"></a><span id="irp_pair_coverage_data"></span><span id="IRP_PAIR_COVERAGE_DATA"></span>IRP 对覆盖率数据

IRP 对覆盖率数据基于 IRP 并发，其中多个 Irp 同时在驱动程序堆栈内处于活动状态。 此数据可帮助确定驱动程序验证过程中的测试覆盖率孔，并可帮助你改进测试以解决驱动程序并发问题。

驱动程序覆盖率工具包监视和报告 1099 MJ 和 MN 函数代码对。

### <a name="span-idsample_irp_coverage_reportspanspan-idsample_irp_coverage_reportspansample-irp-coverage-report"></a><span id="sample_irp_coverage_report"></span><span id="SAMPLE_IRP_COVERAGE_REPORT"></span>示例 IRP 覆盖率报告

以下命令可以生成与下一示例类似的 IRP 覆盖率报告：

```
Getting coverage data
 Data source
 Source Type:  Driver
 Source Name:  \\.\DrvcovControl1
 Device
   Friendly Name : USB Mass Storage Device 
   Class Name    : USB 
   Device ID     : USB\VID_04E8&PID_0100\2151151132436 
   Device #      : 1 
 Devnode #     : 5088 

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

 

