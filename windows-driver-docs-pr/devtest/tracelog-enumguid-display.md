---
title: Tracelog Enumguid 显示
description: Tracelog Enumguid 显示
ms.assetid: 9bb93238-98f7-4422-8434-b4dc105ec008
keywords:
- Tracelog WDK，提供程序
- 提供程序 WDK 软件跟踪
- 跟踪 WDK，提供程序
- -enumguid 命令
- enumguid 命令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36450bb7e1d880260b09d4dfbd312b694cf54fbc
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769697"
---
# <a name="tracelog-enumguid-display"></a>Tracelog Enumguid 显示

提交**tracelog enumguid**命令时，tracelog 将显示正在运行且已使用 Windows 事件跟踪（ETW）[注册](registered-provider.md)的跟踪提供程序的列表。 显示非常有用，但通常不会被误解。

### <a name="span-idwhich_providers_appear_in_the_display_spanspan-idwhich_providers_appear_in_the_display_spanwhich-providers-appear-in-the-display"></a><span id="which_providers_appear_in_the_display_"></span><span id="WHICH_PROVIDERS_APPEAR_IN_THE_DISPLAY_"></span>哪些提供程序显示在显示中？

Tracelog enumguid 显示列出了一些您可以为跟踪会话启用的提供程序，但它不是完整列表。 它仅包括正在运行且已注册 ETW 的跟踪提供程序。

显示内容不包括以下提供程序：

可在系统上使用但未注册的跟踪提供程序，通常是因为它们没有运行。

跟踪提供程序已启用跟踪会话，但当前未运行。 （这通常称为*预启用*或*预注册*的提供程序。）这包括不连续运行的提供程序，如根据需要加载和卸载的 Dll。

内置于 Windows 中的提供程序，包括用于系统会话的提供程序和用于[全局记录器跟踪会话](global-logger-trace-session.md)和[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)的提供程序。

### <a name="span-idthe_logman_query_providers_displayspanspan-idthe_logman_query_providers_displayspanthe-logman-query-providers-display"></a><span id="the_logman_query_providers_display"></span><span id="THE_LOGMAN_QUERY_PROVIDERS_DISPLAY"></span>Logman 查询提供程序显示

Tracelog enumguid 显示与查询提供程序在 Logman （**Logman 查询提供程序**）中的显示效果大不相同，但通常会混淆显示器。

Logman （Logman）是跟踪事件和性能计数器的跟踪控制器。 它包含在 Windows XP 和更高版本的 Windows 中。

Logman 提供程序查询（**Logman 查询提供**程序）显示已向 WMI 注册托管对象格式（MOF）文件的提供程序的列表。 Logman 显示不包含检测到的软件跟踪的提供程序，除非它们也已注册到 WMI。

想要帮助用户查找其提供程序的开发人员有时只注册其 MOF 文件，以使提供程序出现在 Logman 显示器中。 遗憾的是，Logman 查询提供程序和 Tracelog enumguid 显示都不显示系统上所有跟踪提供程序的完整列表。 有关 Logman 的详细信息，请参阅 "帮助和支持中心" 中的 "Logman"。

### <a name="span-idelements_of_the_enumguid_displayspanspan-idelements_of_the_enumguid_displayspanelements-of-the-enumguid-display"></a><span id="elements_of_the_enumguid_display"></span><span id="ELEMENTS_OF_THE_ENUMGUID_DISPLAY"></span>Enumguid 显示元素

Tracelog enumguid 显示中的表包含以下列。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列标题</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Guid.empty</strong></p></td>
<td align="left"><p>跟踪提供程序的<a href="control-guid.md" data-raw-source="[control GUID](control-guid.md)">控件 GUID</a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Enabled</strong></p></td>
<td align="left"><p>显示提供程序当前是否已启用（<strong>TRUE</strong>）或已注册但未启用（<strong>FALSE</strong>）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LoggerId</strong></p></td>
<td align="left"><p>标识跟踪会话。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>级别</strong></p></td>
<td align="left"><p>当前为提供程序设置的级别。 仅在启用了提供程序时有效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>标记</strong></p></td>
<td align="left"><p>当前为提供程序设置的标志。 仅在启用了提供程序时有效。</p></td>
</tr>
</tbody>
</table>

 
如果提供程序已注册但未启用，则它显示在 enumguid 显示器中，但在 "**已启用**" 列中其条目为**FALSE**。

如果提供程序已启用但当前未运行，并且未注册，则它不会显示在 enumguid 显示器中。

### <a name="span-idsample_enumguid_displayspanspan-idsample_enumguid_displayspansample-enumguid-display"></a><span id="sample_enumguid_display"></span><span id="SAMPLE_ENUMGUID_DISPLAY"></span>示例 Enumguid 显示

以下 enumguid 显示已从运行 Windows Server 2003 的计算机复制。 显示的将列出已注册并正在运行的提供程序。 为跟踪启用了一个提供程序（Tracedrv 示例驱动程序）。 [TraceDrv](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/tracing/tracedriver)是设计用于软件跟踪的示例驱动程序，位于 GitHub 上的[Windows 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples)存储库中。

```
c:\Tracelog>tracelog -enumguid
##     Guid                     Enabled  LoggerId Level Flags
------------------------------------------------------------
1046d4b1-fce5-48bc-8def-fd33196af19a     FALSE  0    0    0
196e57d9-49c0-4b3b-ac3a-a8a93ada1938     FALSE  0    0    0
4a8aaa94-cfc4-46a7-8e4e-17bc45608f0a     FALSE  0    0    0
1540ff4c-3fd7-4bba-9938-1d1bf31573a7     FALSE  0    0    0
1fbecc45-c060-4e7c-8a0e-0dbd6116181b     FALSE  0    0    0
f12b1984-4c42-11d3-ab7b-00c04f68fcdc     FALSE  0    0    0
94a984ef-f525-4bf1-be3c-ef374056a592     FALSE  0    0    0
3121cf5d-c5e6-4f37-be86-57083590c333     FALSE  0    0    0
f498b9f5-9e67-446a-b9b8-1442ffaef434     FALSE  0    0    0
e1f65b93-f32a-4ed6-aa72-b039e28f1574     FALSE  0    0    0
dd5ef90a-6398-47a4-ad34-4dcecdef795f     FALSE  0    0    0
e80aa9fe-913d-4ede-af58-73e332dcac8d     FALSE  0    0    0
1b1d4ff4-f27b-4c99-8bd7-da8f1a74051a     FALSE  0    0    0
f33959b4-dbec-11d2-895b-00c04f79ab69     FALSE  0    0    0
cc85922f-db41-11d2-9244-006008269001     FALSE  0    0    0
c92cf544-91b3-4dc0-8e11-c580339a0bf8     FALSE  0    0    0
bba3add2-c229-4cdb-ae2b-57eb6966b0c4     FALSE  0    0    0
8fc7e81a-f733-42e0-9708-cfdae07ed969     FALSE  0    0    0
cddc01e2-fdce-479a-b8ee-3c87053fb55e     FALSE  0    0    0
fc4b0d39-e8be-4a83-a32f-c0c7c4f61ee4     FALSE  0    0    0
fc570986-5967-4641-a6f9-05291bce66c5     FALSE  0    0    0
39a7b5e0-be85-47fc-b9f5-593a659abac1     FALSE  0    0    0
dab01d4d-2d48-477d-b1c3-daad0ce6f06b     FALSE  0    0    0
bca7bd7f-b0bf-4051-99f4-03cfe79664c1     FALSE  0    0    0
d58c126f-b309-11d1-969e-0000f875a5bc      TRUE  2    0    0
d58c126e-b309-11d1-969e-0000f875a5bc     FALSE  0    0    0
58db8e03-0537-45cb-b29b-597f6cbebbfe     FALSE  0    0    0
58db8e03-0537-45cb-b29b-597f6cbebbfd     FALSE  0    0    0
688a5248-f348-4576-86cf-3521c7094614     FALSE  0    0    0
27246e9d-b4df-4f20-b969-736fa49ff6ff    FALSE  0    0    0
```
