---
title: .echotimestamps（显示时间戳）
description: Echotimestamps 命令打开或关闭时间戳信息的显示。
keywords:
- " () 命令显示时间戳"
- 时间戳
- DbgPrint 时间戳
- echotimestamps (显示时间戳) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .echotimestamps (Show Time Stamps)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 6a90f950f01114079424cbd80628d8a259396207
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817905"
---
# <a name="echotimestamps-show-time-stamps"></a>.echotimestamps（显示时间戳）


**Echotimestamps** 命令打开或关闭时间戳信息的显示。

```dbgcmd
.echotimestamps 0 
.echotimestamps 1 
.echotimestamps 
```

## <a name="span-idddk_meta_show_time_stamps_dbgspanspan-idddk_meta_show_time_stamps_dbgspanparameters"></a><span id="ddk_meta_show_time_stamps_dbg"></span><span id="DDK_META_SHOW_TIME_STAMPS_DBG"></span>参数


<span id="_______0______"></span>**0**   
关闭时间戳信息的显示。 这是调试器的默认行为。

<span id="_______1______"></span>**1**   
启用时间戳信息的显示。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 **DbgPrint**、 **KdPrint**、 **DbgPrintEx** 和 **KdPrintEx** 的详细信息，请参阅 [读取和筛选调试消息](reading-and-filtering-debugging-messages.md)中的 "DbgPrint Buffer"。

<a name="remarks"></a>备注
-------

使用不带参数的 **echotimestamps** 命令时，将打开或关闭时间戳的显示，并显示新状态。

如果打开此显示，调试器将显示模块加载、线程创建、异常和其他事件的时间戳。

**DbgPrint**、 **KdPrint**、 **DbgPrintEx** 和 **KdPrintEx** 内核模式例程将格式化字符串发送到主计算机上的缓冲区。 除非已禁用此打印) ，否则该字符串会显示在 [调试器命令窗口](debugger-command-window.md) (中。 还可以通过使用 [**！ dbgprint**](-dbgprint.md) extension 命令显示带格式的字符串。

当使用 **echotimestamps** 打开时间戳的显示时，将显示 **DbgPrint** 缓冲区中每个注释的时间和日期。

 

 





