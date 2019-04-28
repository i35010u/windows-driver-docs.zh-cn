---
title: .echotimestamps（显示时间戳）
description: .Echotimestamps 命令打开或关闭显示器的时间戳信息。
ms.assetid: c70dc71b-83c2-41de-90f3-638e231c0476
keywords:
- 显示时间戳 (.echotimestamps) 命令
- 时间戳
- DbgPrint 时间戳
- .echotimestamps （显示时间戳） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echotimestamps (Show Time Stamps)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8a3351684dc4188c654286079f5bfddfab03a590
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63336803"
---
# <a name="echotimestamps-show-time-stamps"></a>.echotimestamps（显示时间戳）


**.Echotimestamps**命令打开或关闭显示器的时间戳信息。

```dbgcmd
.echotimestamps 0 
.echotimestamps 1 
.echotimestamps 
```

## <a name="span-idddkmetashowtimestampsdbgspanspan-idddkmetashowtimestampsdbgspanparameters"></a><span id="ddk_meta_show_time_stamps_dbg"></span><span id="DDK_META_SHOW_TIME_STAMPS_DBG"></span>参数


<span id="_______0______"></span> **0**   
关闭所显示的时间戳信息。 这是在调试器的默认行为。

<span id="_______1______"></span> **1**   
打开所显示的时间戳信息。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息**DbgPrint**， **KdPrint**， **DbgPrintEx**，以及**KdPrintEx**，请参阅[DbgPrint 缓冲区](reading-and-filtering-debugging-messages.md#the-dbgprint-buffer)或，请参阅 Microsoft Windows Driver Kit (WDK) 文档。

<a name="remarks"></a>备注
-------

当你使用 **.echotimestamps**命令不带参数，显示的时间戳打开或关闭，并显示新状态。

如果打开此显示时，调试器将显示模块加载、 线程创建、 异常和其他事件时间的戳。

**DbgPrint**， **KdPrint**， **DbgPrintEx**，以及**KdPrintEx**内核模式例程将格式化的字符串发送到主机上的缓冲区计算机。 字符串显示在[调试器命令窗口](debugger-command-window.md)（除非禁用了此类打印）。 此外可以通过使用显示带格式的字符串[ **！ dbgprint** ](-dbgprint.md)扩展命令。

当你使用 **.echotimestamps**开启的时间戳、 时间和日期的每个注释中显示**DbgPrint**显示缓冲区。

 

 





