---
title: Cleanup4CtlDeviceRegistered 规则 (kmdf)
description: Cleanup4CtlDeviceRegistered 规则指定，是否插即用 (PnP) 驱动程序调用 WdfDeviceCreate 控制设备对象，该驱动程序必须注册一个必需的事件回调函数。
ms.assetid: f439ec36-f7af-46e5-8ddd-11e444bf36da
ms.date: 05/21/2018
keywords:
- Cleanup4CtlDeviceRegistered 规则 (kmdf)
topic_type:
- apiref
api_name:
- Cleanup4CtlDeviceRegistered
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0e18af64c81953045854b429c117b82e07f814c6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340400"
---
# <a name="cleanup4ctldeviceregistered-rule-kmdf"></a>Cleanup4CtlDeviceRegistered 规则 (kmdf)


**Cleanup4CtlDeviceRegistered**规则指定如果插即用 (PnP) 驱动程序调用[ **WdfDeviceCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff545926)控件设备对象，该驱动程序必须注册所需的事件回调函数之一。

事件回调函数可以是以下值之一：

[*EvtCleanupCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540840)或[ *EvtDestroyCallback* ](https://msdn.microsoft.com/library/windows/hardware/ff540841)中[ **WDF\_对象\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff552400)控制设备的结构- [ *EvtDeviceSelfManagedIoCleanup* ](https://msdn.microsoft.com/library/windows/hardware/ff540898)中[ **WDF\_PNPPOWER\_事件\_回调**](https://msdn.microsoft.com/library/windows/hardware/ff552416)结构

|              |      |
|--------------|------|
| 驱动程序模型 | KMDF |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>Cleanup4CtlDeviceRegistered</strong>规则。</p>
使用以下步骤来分析你的代码：
<ol>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://msdn.microsoft.com/library/windows/hardware/hh454281#preparing-your-source-code)">准备你的代码 （使用角色类型声明）。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://msdn.microsoft.com/library/windows/hardware/hh454281#running-static-driver-verifier)">运行的 Static Driver Verifier。</a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://msdn.microsoft.com/library/windows/hardware/hh454281#viewing-and-analyzing-the-results)">查看和分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/hh454281" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://msdn.microsoft.com/library/windows/hardware/hh454281)">以找到缺陷驱动程序中使用 Static Driver Verifier</a>。</p></td>
</tr>
</tbody>
</table>









