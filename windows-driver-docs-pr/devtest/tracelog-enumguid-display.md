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
ms.openlocfilehash: e94a41767a6fe440f0db0f45e1f47108d2f4d112
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576480"
---
# <a name="tracelog-enumguid-display"></a>Tracelog Enumguid 显示

提交时**tracelog enumguid**命令时，Tracelog 显示一系列的跟踪提供程序正在运行并且已[注册](registered-provider.md)使用事件跟踪 Windows (ETW)。 显示是非常有用，但它通常被错误解释。

### <a name="span-idwhichprovidersappearinthedisplayspanspan-idwhichprovidersappearinthedisplayspanwhich-providers-appear-in-the-display"></a><span id="which_providers_appear_in_the_display_"></span><span id="WHICH_PROVIDERS_APPEAR_IN_THE_DISPLAY_"></span>显示中显示哪些提供程序？

Tracelog enumguid 显示列出了一些跟踪会话，可以启用的提供程序，但它不是完整的列表。 它包括仅跟踪提供程序正在运行并且已向 ETW 注册。

显示不包括以下提供程序：

通常跟踪提供程序可在系统上，但未注册，因为它们未运行。

跟踪提供程序，用于跟踪会话被启用，但不是当前正在运行。 (这些测试通常称为*预先启用*或*预注册*提供程序。)这包括如 Dll 的加载和卸载根据需要并不连续，运行的提供程序。

内置于 Windows，包括系统会话和提供程序提供程序的提供程序[全局记录器跟踪会话](global-logger-trace-session.md)并[NT 内核记录器跟踪会话](nt-kernel-logger-trace-session.md)。

### <a name="span-idthelogmanqueryprovidersdisplayspanspan-idthelogmanqueryprovidersdisplayspanthe-logman-query-providers-display"></a><span id="the_logman_query_providers_display"></span><span id="THE_LOGMAN_QUERY_PROVIDERS_DISPLAY"></span>Logman 查询提供程序显示

Tracelog enumguid 显示却大不相同的查询提供程序显示 Logman 中 (**logman 查询提供程序**)，尽管显示通常容易混淆。

Logman (logman.exe) 是跟踪事件和性能计数器跟踪控制器。 它包含在 Windows XP 和更高版本的 Windows。

Logman 提供程序的查询 (**logman 查询提供程序**) 显示一系列已注册到 WMI 托管对象格式 (MOF) 文件的提供程序。 Logman 显示不包括检测的软件跟踪提供程序，除非它们已注册 WMI。

开发人员想要帮助用户有时会查找其提供程序注册他们的 MOF 文件只是为了使 Logman 显示中显示的提供程序。 遗憾的是，Logman 查询提供程序显示和 Tracelog enumguid 显示器都不是在系统上的所有跟踪提供程序的完整列表。 Logman 有关的详细信息，请参阅帮助和支持中心中的"Logman"。

### <a name="span-idelementsoftheenumguiddisplayspanspan-idelementsoftheenumguiddisplayspanelements-of-the-enumguid-display"></a><span id="elements_of_the_enumguid_display"></span><span id="ELEMENTS_OF_THE_ENUMGUID_DISPLAY"></span>元素的 Enumguid 显示

Tracelog enumguid 显示中的表包括以下列。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">列标题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>guid</strong></p></td>
<td align="left"><p><a href="control-guid.md" data-raw-source="[control GUID](control-guid.md)">控制 GUID</a>跟踪提供程序</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Enabled</strong></p></td>
<td align="left"><p>显示提供程序当前是否启用了 (<strong>，则返回 TRUE</strong>) 或已注册但未启用 (<strong>FALSE</strong>)。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>LoggerId</strong></p></td>
<td align="left"><p>标识跟踪会话。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Level</strong></p></td>
<td align="left"><p>当前设置为提供程序的级别。 仅在启用的提供程序时才有效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>标志</strong></p></td>
<td align="left"><p>当前设置为提供程序的标志。 仅在启用的提供程序时才有效。</p></td>
</tr>
</tbody>
</table>

 
如果提供程序是已注册但未启用，则它显示在 enumguid 显示，但在其条目**已启用**列为**FALSE**。

如果提供程序已启用，但当前未运行且为，因此，未注册，则它不会不出现在 enumguid 显示。

### <a name="span-idsampleenumguiddisplayspanspan-idsampleenumguiddisplayspansample-enumguid-display"></a><span id="sample_enumguid_display"></span><span id="SAMPLE_ENUMGUID_DISPLAY"></span>示例 Enumguid 显示

以下 enumguid 显示已从运行 Windows Server 2003 的计算机复制。 仅显示已注册并正在运行的提供程序。 一个提供程序，Tracedrv 示例驱动程序，可用于跟踪。 [TraceDrv](https://go.microsoft.com/fwlink/p/?LinkId=617726)，为软件跟踪设计的一个示例驱动程序现已推出[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)GitHub 上的存储库。

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
