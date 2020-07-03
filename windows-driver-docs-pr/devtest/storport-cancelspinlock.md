---
title: CancelSpinLock 规则（storport）
description: CancelSpinLock 规则（Storport）规则验证对 IoAcquireCancelSpinLock 的每个调用是否立即后跟对 IoReleaseCancelSpinLock 的调用。
ms.assetid: 36DF0FF0-03CB-4AA1-BD3A-0B7B32AEE3DD
ms.date: 05/21/2018
keywords:
- CancelSpinLock 规则（storport）
topic_type:
- apiref
api_name:
- CancelSpinLock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f58ae2329ce72c1bc5cdf14cbed240841f5bc00b
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917759"
---
# <a name="cancelspinlock-rule-storport"></a>CancelSpinLock 规则（storport）


**CancelSpinLock 规则（Storport）** 规则验证对[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85))的每个调用是否立即后跟对[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))的调用。

如果不首先获取 cancel 自旋锁，则不得调用[**IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85)) 。 此外，当微型端口回调例程退出时，它不得持有任何 cancel 自旋锁

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>CancelSpinLock</strong>规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code)">准备你的代码（使用角色类型声明）。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](https://docs.microsoft.com/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoAcquireCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff548196(v=vs.85)) 
[ **IoReleaseCancelSpinLock**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549550(v=vs.85))
 

 





