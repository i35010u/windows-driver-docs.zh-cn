---
title: 调试 \_ 筛选器 \_ XXX
description: 调试 \_ 筛选器 \_ XXX
ms.date: 12/07/2017
keywords:
- DEBUG_FILTER_XXX Windows 调试
topic_type:
- apiref
api_name:
- DEBUG_FILTER_XXX
api_location:
- DbgEng.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.openlocfilehash: 4d10ba383fa759b26b095d6df8665903127af369
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838235"
---
# <a name="debug_filter_xxx"></a>调试 \_ 筛选器 \_ XXX


调试 \_ 筛选器 \_ *XXX* 常量用于三个不同目的：指定单个特定的事件筛选器、指定事件筛选器的中断状态以及指定异常筛选器的处理状态。

### <a name="span-idspecific_event_filterspanspan-idspecific_event_filterspanspecific-event-filter"></a><span id="specific_event_filter"></span><span id="SPECIFIC_EVENT_FILTER"></span>特定事件筛选器

以下常量用于指定特定的事件筛选器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">事件</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_CREATE_THREAD</p></td>
<td align="left"><p>创建线程</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_EXIT_THREAD</p></td>
<td align="left"><p>退出线程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_CREATE_PROCESS</p></td>
<td align="left"><p>创建进程</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_EXIT_PROCESS</p></td>
<td align="left"><p>退出进程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_LOAD_MODULE</p></td>
<td align="left"><p>加载模块</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_UNLOAD_MODULE</p></td>
<td align="left"><p>卸载模块</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_SYSTEM_ERROR</p></td>
<td align="left"><p>系统错误</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_INITIAL_BREAKPOINT</p></td>
<td align="left"><p>初始断点</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_INITIAL_MODULE_LOAD</p></td>
<td align="left"><p>初始模块加载</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_DEBUGGEE_OUTPUT</p></td>
<td align="left"><p>目标输出</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idbreak_statusspanspan-idbreak_statusspanbreak-status"></a><span id="break_status"></span><span id="BREAK_STATUS"></span>中断状态

以下常量用于指定事件筛选器的中断状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_BREAK</p></td>
<td align="left"><p>事件将中断到调试器。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_SECOND_CHANCE_BREAK</p></td>
<td align="left"><p>如果是第二次异常，事件会中断到调试器。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_OUTPUT</p></td>
<td align="left"><p>事件的通知将打印到调试器控制台。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_IGNORE</p></td>
<td align="left"><p>忽略此事件。</p></td>
</tr>
</tbody>
</table>

 

此外，对于任意异常筛选器，将中断状态设置为调试 \_ 筛选器将 \_ 删除事件筛选器。

### <a name="span-idhandling_statusspanspan-idhandling_statusspanhandling-status"></a><span id="handling_status"></span><span id="HANDLING_STATUS"></span>处理状态

以下常量用于指定异常筛选器的处理状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>DEBUG_FILTER_GO_HANDLED</p></td>
<td align="left"><p>已处理异常。</p></td>
</tr>
<tr class="even">
<td align="left"><p>DEBUG_FILTER_GO_NOT_HANDLED</p></td>
<td align="left"><p>异常尚未处理。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">DbgEng (包含 DbgEng) </td>
</tr>
</tbody>
</table>

 

 





