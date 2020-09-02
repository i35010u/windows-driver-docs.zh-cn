---
title: 'StorPortNotification2 规则 (storport) '
description: 此规则验证对 StorPortNotification 的调用是否仅使用允许的 (即) 通知类型。
ms.assetid: 74363E6D-1D1B-484D-A558-8996DFE02FA8
ms.date: 05/21/2018
keywords:
- 'StorPortNotification2 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortNotification2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bf017ab84636c9218f24775c40cc410393e64850
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383343"
---
# <a name="storportnotification2-rule-storport"></a>StorPortNotification2 规则 (storport) 


此规则验证对 **StorPortNotification** 的调用是否仅使用允许的 (即) 通知类型。

允许的通知类型为：

**BufferOverrunDetected** 
**BusChangeDetected** 
**LinkDown** 
**LinkUp** 
**QueryTickCount** 
**RequestComplete** 
**RequestTimerCall** 
**ResetDetected** 
**Register-wmievent** 
**WMIReregister**

**驱动程序模型： Storport**

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortNotification2</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**StorPortNotification**](/windows-hardware/drivers/ddi/storport/nf-storport-storportnotification)