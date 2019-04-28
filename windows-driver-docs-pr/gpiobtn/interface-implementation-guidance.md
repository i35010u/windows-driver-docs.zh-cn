---
title: 接口实现指南
description: 本部分提供了接口实现的指南。
ms.assetid: E97A880F-0422-432C-8567-444CA6FD2980
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 37285e04fe0e09a4353a392b92e1fdff569774eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344611"
---
# <a name="interface-implementation-guidance"></a>接口实现指南


本部分提供了接口实现的指南。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


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
<td align="left"><p><a href="available-interfaces-and-related-apis.md" data-raw-source="[Available interfaces and related APIs](available-interfaces-and-related-apis.md)">可用接口和相关的 Api</a></p></td>
<td align="left"><p>有三个 GPIO 接口： 一个用于每个设备。 每个接口的 guid 引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="indicator-implementation.md" data-raw-source="[Indicator implementation](indicator-implementation.md)">指示器实现</a></p></td>
<td align="left"><p>本主题介绍指示器实现。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="button-implementation.md" data-raw-source="[Button implementation](button-implementation.md)">按钮实现</a></p></td>
<td align="left"><p>我们建议用于按钮和状态指示器的物理 GPIO 资源。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idsystemstatespanspan-idsystemstatespanspan-idsystemstatespansystem-state"></a><span id="System_state"></span><span id="system_state"></span><span id="SYSTEM_STATE"></span>系统状态


在向上的位置是支持的负载上的收件箱驱动程序的所有按钮的默认状态。

通过使用接口的第一个提示切换到状态的向下 （由索引） 指定的按钮。

便携式计算机/盖板模式指示器的默认状态是静态图像。

停靠的模式指示器的默认状态是移除。

通过使用接口的第一个提示切换为其他状态指示器。

若要查询的状态，可以按如下所示使用 GetSystemMetric API:

``` syntax
int WINAPI GetSystemMetrics(
  _In_  int nIndex
);
```

可用于指示符的参数：

-   SM\_SYSTEMDOCKED 停靠状态。 调用会返回 0 停靠模式和非零值否则。
-   SM\_CONVERTIBLESLATEMODE 盖板模式。 调用会返回 0 盖板模式和非零值否则。

## <a name="span-idnotificationsspanspan-idnotificationsspanspan-idnotificationsspannotifications"></a><span id="Notifications"></span><span id="notifications"></span><span id="NOTIFICATIONS"></span>通知


当任一系统指标 SM\_CONVERTIBLESLATEMODE 或 SM\_SYSTEMDOCKED 更改使用 WM 系统发送广播的消息\_SETTINGCHANGE。

WM LPARAM\_SETTINGCHANGE 消息指示哪个系统指标已通过使用"ConvertibleSlateMode"或"SystemDockMode"的字符串。

 

 




