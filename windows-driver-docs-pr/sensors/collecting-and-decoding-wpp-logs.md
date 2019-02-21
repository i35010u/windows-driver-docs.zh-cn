---
title: 收集和解码 WPP 日志
description: 本主题提供有关收集和解码为传感器类扩展 (CX) 跟踪提供程序的 Windows 软件跟踪预处理器 (WPP) 日志的信息。
ms.assetid: 174CDE37-D0D1-44BF-AD50-5A90C989FDE2
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: ac909cb176bd644fdaa76895d56ad1c62e3dd014
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545351"
---
# <a name="collecting-and-decoding-wpp-logs"></a>收集和解码 WPP 日志


本主题提供有关收集和解码为传感器类扩展 (CX) 跟踪提供程序的 Windows 软件跟踪预处理器 (WPP) 日志的信息。

WPP 提供方法来跟踪称为跟踪提供程序的软件组件的操作。 以下是包含要解码的 WPP 日志的 PDB 文件。

-   SensorsCx.pdb

-   SensorsUtilsV2.pdb

跟踪日志工具用于收集 WPP 日志。 有关详细信息，请参阅[Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx)。 有关跟踪概念，如跟踪 Guid，跟踪标志、 跟踪级别或 PDB 文件的详细信息，请参阅[跟踪工具概念](https://msdn.microsoft.com/library/windows/hardware/ff553975.aspx)。

## <a name="tracing-guid"></a>跟踪的 GUID


下面的 GUID 标识传感器 V2 堆栈中的 CX 驱动程序的跟踪提供程序。 使用此 GUID 的跟踪日志的详细信息，请参阅[Tracelog](https://msdn.microsoft.com/library/windows/hardware/ff552994.aspx)。

``` syntax
c88b592b-6090-480f-a839-ca2434de5844
```

## <a name="trace-flags"></a>跟踪标志


传感器类扩展定义以下 WPP\_控制\_GUID 跟踪标志：

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


以下跟踪级别定义的跟踪日志使用情况。 有关如何使用这些详细信息，请参阅**级别**tracelog 语法中的参数。

``` syntax
TRACE_LEVEL_FATAL           1
TRACE_LEVEL_ERROR           2
TRACE_LEVEL_WARNING         3
TRACE_LEVEL_INFORMATION     4
TRACE_LEVEL_VERBOSE         5
TRACE_LEVEL_PERF            6
```

## <a name="tracelog-macros"></a>Tracelog 宏


以下是使用其关联的跟踪级别和跟踪标志 WPP 宏。 消息参数是为 printf 函数定义的标准格式字符串。 合作伙伴还可以使用 WPP 扩展格式字符串。 有关详细信息信息，请参阅[WPP 扩展格式字符串](https://go.microsoft.com/fwlink/p/?linkid=324276)MSD 上的主题。 换行字符也包含在消息因此"\\n"不是必需的。

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
<th>Flag</th>
<th>参数</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>TraceFatal</p></td>
<td><p>TRACE_LEVEL_FATAL</p></td>
<td><p>严重</p></td>
<td><p>MSG</p></td>
</tr>
<tr class="even">
<td><p>TraceError</p></td>
<td><p>TRACE_LEVEL_ERROR</p></td>
<td><p>错误</p></td>
<td><p>MSG</p></td>
</tr>
<tr class="odd">
<td><p>TraceWarning</p></td>
<td><p>TRACE_LEVEL_WARNING</p></td>
<td><p>警告</p></td>
<td><p>MSG</p></td>
</tr>
<tr class="even">
<td><p>TraceInformation</p></td>
<td><p>TRACE_LEVEL_INFORMATION</p></td>
<td><p>信息</p></td>
<td><p>MSG</p></td>
</tr>
<tr class="odd">
<td><p>TraceVerbos</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>Verbose</p></td>
<td><p>MSG</p></td>
</tr>
<tr class="even">
<td><p>TracePerformance</p></td>
<td><p>TRACE_LEVEL_PERF</p></td>
<td><p></p></td>
<td><p>标志消息</p></td>
</tr>
<tr class="odd">
<td><p>TraceData</p></td>
<td><p>TRACE_LEVEL_VERBOSE</p></td>
<td><p>DataFlow</p></td>
<td><p>MSG</p></td>
</tr>
<tr class="even">
<td><p>TraceDriverStatus</p></td>
<td><p>TRACE_LEVEL_INFORMATION</p></td>
<td><p>DriverStatus</p></td>
<td><p>MSG</p></td>
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


Tracefmt 工具用于解码 ETL 日志。 有关此工具的详细信息，请参阅[Tracefmt](https://go.microsoft.com/fwlink/p/?linkid=324212)。

如果你想要执行更全面的测试的传感器驱动程序，请参阅 [测试通用传感器驱动程序] (测试-您的世界的传感器-driver.md。

 

 




