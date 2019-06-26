---
title: 驱动程序覆盖范围工具包概述
description: 驱动程序覆盖范围工具包概述
ms.assetid: eead0c9a-fc26-4777-b19a-e97b898e28a2
keywords:
- 驱动程序覆盖范围工具包 WDK，有关驱动程序覆盖范围工具包
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d3f662c400ef8bc44f040c6d562902b7ec51b4b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361273"
---
# <a name="overview-of-the-driver-coverage-toolkit"></a>驱动程序覆盖范围工具包概述


**请注意**  的驱动程序覆盖范围工具包不再需要在 Windows 10 中，安装程序不再包含在 WDK 中。 若要执行此处所述在 Windows 10 中的任务，请改用[Driver Verifier](driver-verifier.md)并[IRP 日志记录](irp-logging.md)。

 

驱动程序覆盖范围工具包监视和报告的 I/O 请求数据包 (Irp)，进入或离开驱动程序堆栈的一个或多个指定的设备。 覆盖率数据收集[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)为这些设备。 驱动程序覆盖范围工具用于启用或禁用指定设备上的 IRP 覆盖，以及生成报表从覆盖率数据。

驱动程序覆盖范围工具包收集并报告 IRP 覆盖率数据基于三个度量值：

<span id="Major__MJ__IRP_Function_Codes"></span><span id="major__mj__irp_function_codes"></span><span id="MAJOR__MJ__IRP_FUNCTION_CODES"></span>主要 (MJ) IRP 函数代码  
处于活动状态的设备驱动程序堆栈内的 Irp 的 MJ 函数代码的计数。 驱动程序覆盖范围工具包收集 12 MJ 函数代码的数据。 有关这些函数代码的详细信息，请参阅[IRP 主要函数代码](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-major-function-codes)。

<span id="Major__MJ__and_Minor__MN__IRP_Function_Codes"></span><span id="major__mj__and_minor__mn__irp_function_codes"></span><span id="MAJOR__MJ__AND_MINOR__MN__IRP_FUNCTION_CODES"></span>(MJ) 主要和次要的 (MN) IRP 函数代码  
MJ IRP 函数代码，连同的 Irp 处于活动状态的设备驱动程序堆栈内的其从属 MN 函数代码的计数。 驱动程序覆盖范围工具包收集 52 MJ 和 MN 函数代码的数据。

<span id="IRP_Pairs"></span><span id="irp_pairs"></span><span id="IRP_PAIRS"></span>IRP 对  
已在设备驱动程序堆栈中并发活动 MJ 和 MJ/MN IRP 函数代码的计数。 此计数反映的次数单独 Irp 进入或离开在同一时间的驱动程序堆栈。 驱动程序覆盖范围工具包收集 1099 MJ 和 MN 函数代码对数据。

有关 IRP 函数代码的详细信息，请参阅[IRP 函数代码](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550706(v=vs.85))。

### <a name="span-idirpcoveragedataspanspan-idirpcoveragedataspanirp-coverage-data"></a><span id="irp_coverage_data"></span><span id="IRP_COVERAGE_DATA"></span>IRP 覆盖率数据

每当 IRP 进入或离开由监视的设备驱动程序堆栈[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)，筛选器驱动程序递增及其与 IRP 相关的计数器。 驱动程序覆盖范围筛选器驱动程序监视 active Irp 驱动程序堆栈，而不考虑如何 Irp 发起内。 因此，监视窗口的筛选器驱动程序的 IRP 介绍的所有驱动程序堆栈中的下列筛选器驱动程序立即分层。

[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)时它首先监视驱动程序堆栈内的 IRP 递增及其 IRP 的计数器。 如果 IRP 源于驱动程序堆栈之外，驱动程序覆盖范围筛选器驱动程序会增加其计数器的 IRP 在 IRP 进入堆栈的时间。 如果 IRP 源自驱动程序堆栈中的驱动程序，筛选器驱动程序将 IRP 离开驱动程序堆栈时递增其计数器。

下图显示了设备驱动程序堆栈中的 IRP 流量的示例。

![说明中的设备驱动程序堆栈的 i/o 请求数据包 (irp) 流量的关系图](images/coverage-3.png)

在此示例中，[驱动程序覆盖范围筛选器驱动程序](driver-coverage-filter-driver.md)监视以下 Irp:

-   IRP A，只需进入驱动程序堆栈。

-   IRP B，即将退出驱动程序堆栈。

驱动程序覆盖范围筛选器驱动程序对于这两个 Irp 的递增其 MN 和 MN/MJ 函数代码计数器。 此外，因为这两个 Irp A 和 B 中保持活动状态的驱动程序堆栈，驱动程序覆盖范围筛选器驱动程序将递增 {IRP A、 B IRP} 的元组的 IRP 对计数器。

### <a name="span-idirppaircoveragedataspanspan-idirppaircoveragedataspanirp-pair-coverage-data"></a><span id="irp_pair_coverage_data"></span><span id="IRP_PAIR_COVERAGE_DATA"></span>IRP 对覆盖率数据

IRP 对覆盖率数据基于 IRP 的并发程度，在其中多个 Irp 中保持活动状态的驱动程序堆栈在同一时间。 此数据可以帮助确定测试覆盖率漏洞在驱动程序验证期间，可帮助提高你的测试解决驱动程序并发问题。

驱动程序覆盖范围工具包监视器和 1099 MJ 和 MN 函数代码对上的报表。

### <a name="span-idsampleirpcoveragereportspanspan-idsampleirpcoveragereportspansample-irp-coverage-report"></a><span id="sample_irp_coverage_report"></span><span id="SAMPLE_IRP_COVERAGE_REPORT"></span>示例 IRP 覆盖范围报表

以下命令生成类似于下一个示例 IRP 覆盖率报告：

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

 

 





