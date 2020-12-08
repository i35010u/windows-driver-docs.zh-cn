---
title: 接口实现指南
description: 本部分提供有关接口实现的指南。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2b688e79cf4496e3755a51d1aaff1c6891b8890e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830601"
---
# <a name="interface-implementation-guidance"></a>接口实现指南


本部分提供有关接口实现的指南。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="available-interfaces-and-related-apis.md" data-raw-source="[Available interfaces and related APIs](available-interfaces-and-related-apis.md)">可用接口和相关 API</a></p></td>
<td align="left"><p>有三种 GPIO 接口：每个设备一个。 每个接口都由一个 GUID 引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="indicator-implementation.md" data-raw-source="[Indicator implementation](indicator-implementation.md)">指示器实现</a></p></td>
<td align="left"><p>本主题介绍指标实现。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="button-implementation.md" data-raw-source="[Button implementation](button-implementation.md)">按钮实现</a></p></td>
<td align="left"><p>建议为按钮和状态指示器使用物理 GPIO 资源。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsystem_statespanspan-idsystem_statespanspan-idsystem_statespansystem-state"></a><span id="System_state"></span><span id="system_state"></span><span id="SYSTEM_STATE"></span>系统状态


收件箱驱动程序所支持的所有按钮的默认状态都处于 "正常" 状态。

第一次通过使用接口切换指定按钮 (按索引) 到关闭状态。

笔记本电脑/石板模式指示器的默认状态为石板。

停靠模式指示器的默认状态为 "未停靠"。

使用接口将指示器切换到其他状态的第一个指示。

若要查询状态，可以使用 GetSystemMetric API，如下所示：

``` syntax
int WINAPI GetSystemMetrics(
  _In_  int nIndex
);
```

可用于指示器的参数：

-   SM \_ SYSTEMDOCKED 的停靠状态。 对于取消停靠模式，调用返回 0; 否则返回非零值。
-   \_用于石板模式的 SM CONVERTIBLESLATEMODE。 对于石板模式，调用返回 0; 否则返回非零值。

## <a name="span-idnotificationsspanspan-idnotificationsspanspan-idnotificationsspannotifications"></a><span id="Notifications"></span><span id="notifications"></span><span id="NOTIFICATIONS"></span>报警


当系统指标 SM \_ CONVERTIBLESLATEMODE 或 sm \_ SYSTEMDOCKED 发生变化时，系统会使用 WM SETTINGCHANGE 发送一条广播消息 \_ 。

WM SETTINGCHANGE 消息的 LPARAM \_ 通过使用 "ConvertibleSlateMode" 或 "SystemDockMode" 的字符串来指示已更改的系统指标。

 

 




