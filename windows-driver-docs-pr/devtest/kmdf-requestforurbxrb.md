---
title: RequestForUrbXrb 规则 (kmdf)
ms.assetid: 8BFFB73D-106A-4CD0-93F2-D295D969729E
ms.date: 05/21/2018
description: ''
keywords:
- RequestForUrbXrb 规则 (kmdf)
topic_type:
- apiref
api_name:
- RequestForUrbXrb
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5f860743c2ffe9810321b4ac10e80ba83b21558a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526252"
---
# <a name="requestforurbxrb-rule-kmdf"></a>RequestForUrbXrb 规则 (kmdf)


如果客户端驱动程序调用[ **WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428) ，并指定客户端约定版本 USBD\_客户端\_协定\_版本\_602 中 WDF\_USB\_设备\_创建\_（以适用于 Windows 8 使用 USB 驱动程序堆栈的新功能） 的配置结构，DDIs，使用 URB 在内部将仅使用*URB 上下文*如果满足任何需要满足以下先决条件：

-   请求参数具有 Wdf 设备在其父对象树中。
-   请求通过 I/O 队列表示。
-   请求其父对象树中有另一个 I/O 队列表示请求。

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
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff552808" data-raw-source="[Static Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff552808)">Static Driver Verifier</a>并指定<strong>RequestForUrbXrb</strong>规则。</p>
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

<a name="applies-to"></a>适用于
----------

[**WdfRequestCreate**](https://msdn.microsoft.com/library/windows/hardware/ff549951)
[**WdfUsbTargetDeviceCreateWithParameters** ](https://msdn.microsoft.com/library/windows/hardware/hh439428) 
 [ **WdfUsbTargetDeviceFormatRequestForControlTransfer**](https://msdn.microsoft.com/library/windows/hardware/ff550082)
[**WdfUsbTargetDeviceFormatRequestForString** ](https://msdn.microsoft.com/library/windows/hardware/ff550086) 
[ **WdfUsbTargetDeviceSendControlTransferSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff550104)
[**WdfUsbTargetPipeAbortSynchronously** ](https://msdn.microsoft.com/library/windows/hardware/ff551129)
 [ **WdfUsbTargetPipeFormatRequestForAbort**](https://msdn.microsoft.com/library/windows/hardware/ff551132)
[**WdfUsbTargetPipeFormatRequestForReset** ](https://msdn.microsoft.com/library/windows/hardware/ff551138) 
 [ **WdfUsbTargetPipeResetSynchronously**](https://msdn.microsoft.com/library/windows/hardware/ff551156)
 

 





