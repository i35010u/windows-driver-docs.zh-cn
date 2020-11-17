---
title: 收集和解码 WPP 日志
description: 本主题提供有关为传感器类扩展 (CX) 跟踪提供程序收集和解码 Windows 软件跟踪预处理器 (WPP) 日志的信息。
ms.assetid: 174CDE37-D0D1-44BF-AD50-5A90C989FDE2
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 318e6a1c358be9c0aca247af915a6b4300ab2e13
ms.sourcegitcommit: ea3215e9d5afe073ed6d01fb6dddf31d95ef3b63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2020
ms.locfileid: "94673769"
---
# <a name="collecting-and-decoding-wpp-logs"></a>收集和解码 WPP 日志


本主题提供有关为传感器类扩展 (CX) 跟踪提供程序收集和解码 Windows 软件跟踪预处理器 (WPP) 日志的信息。

WPP 提供了跟踪软件组件（称为跟踪提供程序）的操作的方法。 下面是用于解码 WPP 日志的 PDB 文件。

-   SensorsCx .pdb

-   SensorsUtilsV2 .pdb

Tracelog 工具用于收集 WPP 日志。 有关详细信息，请参阅 [Tracelog](../devtest/tracelog.md)。 有关跟踪 Guid、跟踪标志、跟踪级别或 PDB 文件等跟踪概念的详细信息，请参阅 [跟踪工具的概念](../devtest/tracing-tool-concepts.md)。

## <a name="tracing-guid"></a>跟踪 GUID


以下 GUID 标识传感器 V2 堆栈中 CX 驱动程序的跟踪提供程序。 有关将此 GUID 用于 tracelog 的详细信息，请参阅 [tracelog](../devtest/tracelog.md)。

``` syntax
c88b592b-6090-480f-a839-ca2434de5844
```

## <a name="trace-flags"></a>跟踪标志


传感器类扩展定义以下 WPP \_ 控制 \_ guid 跟踪标志：

``` syntax
EntryExit
DataFlow
Verbose
Information
Warning
Error
Fatal
DriverStatus
```

## <a name="trace-levels"></a>跟踪级别


为使用 tracelog 定义了以下跟踪级别。 有关如何使用这些方法的详细信息，请参阅 tracelog 语法中的 **level** 参数。

``` syntax
TRACE_LEVEL_FATAL           1
TRACE_LEVEL_ERROR           2
TRACE_LEVEL_WARNING         3
TRACE_LEVEL_INFORMATION     4
TRACE_LEVEL_VERBOSE         5
TRACE_LEVEL_PERF            6
```

## <a name="tracelog-macros"></a>Tracelog 宏


下面是 WPP 宏及其关联的跟踪级别和跟踪标志。 MSG 参数是为 printf 函数定义的标准格式字符串。 合作伙伴还可以使用 WPP 扩展格式字符串。 有关此内容的详细信息，请参阅 MSD 上的 [WPP 扩展格式字符串](../devtest/what-are-the-wpp-extended-format-specification-strings-.md) 主题。 换行符也包含在消息中，因此 \\ 不需要 "n"。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>宏</th>
<th>级别</th>
<th>标志</th>
<th>参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TraceFatal</p></td>
<td><p>TRACE_LEVEL_FATAL</p></td>
<td><p>出现</p></td>
<td><p>缺少</p></td>
</tr>
<tr class="even">
<td><p>TraceError</p></td>
<td><p>TRACE_LEVEL_ERROR</p></td>
<td><p>错误</p></td>
<td><p>缺少</p></td>
</tr>
<tr class="odd">
<td><p>TraceWarning</p></td>
<td><p>TRACE_LEVEL_WARNING</p></td>
<td><p>警告</p></td>
<td><p>缺少</p></td>
</tr>
<tr class="even">
<td><p>Tracesource.traceinformation</p></td>
<td><p>TRACE_LEVEL_INFORMATION</p></td>
<td><p>信息</p></td>
<td><p>缺少</p></td>
</tr>
<tr class="odd">
<td><p>TraceVerbos</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>“详细”</p></td>
<td><p>缺少</p></td>
</tr>
<tr class="even">
<td><p>TracePerformance</p></td>
<td><p>TRACE_LEVEL_PERF</p></td>
<td><p></p></td>
<td><p>标志，MSG</p></td>
</tr>
<tr class="odd">
<td><p>TraceData</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>数据流</p></td>
<td><p>缺少</p></td>
</tr>
<tr class="even">
<td><p>TraceDriverStatus</p></td>
<td><p>TRACE_LEVEL_INFORMATION</p></td>
<td><p>DriverStatus</p></td>
<td><p>缺少</p></td>
</tr>
<tr class="odd">
<td><p>CLX_FunctionEnter</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>CLX_FunctionExit</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>NTSTATUS</p></td>
</tr>
<tr class="odd">
<td><p>SENSOR_FunctionEnter</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>不适用</p></td>
</tr>
<tr class="even">
<td><p>SENSOR_FunctionExit</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>EntryExit</p></td>
<td><p>NTSTATUS</p></td>
</tr>
</tbody>
</table>

 

## <a name="decoding-etl-logs"></a>解码 ETL 日志


Tracefmt 工具用于解码 ETL 日志。 有关此工具的详细信息，请参阅 [Tracefmt](../devtest/tracefmt.md)。

如果要对传感器驱动程序进行更广泛的测试，请参阅 [测试通用传感器驱动程序](test-your-universal-sensor-driver.md)。

