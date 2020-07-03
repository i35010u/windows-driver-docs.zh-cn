---
title: WdfWaitlockRelease 规则（kmdf）
description: WdfWaitlockRelease 规则指定对 WdfWaitLockAcquire 和 WdfWaitLockRelease 的调用在 KMDF 事件回调函数内按平衡方式使用。
ms.assetid: 4ac60469-b9a3-4777-865b-f03d5a4da8ed
ms.date: 05/21/2018
keywords:
- WdfWaitlockRelease 规则（kmdf）
topic_type:
- apiref
api_name:
- WdfWaitlockRelease
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 5a6fe4681df50c4468fe2a143106f9d238f861ef
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85918111"
---
# <a name="wdfwaitlockrelease-rule-kmdf"></a>WdfWaitlockRelease 规则（kmdf）


**WdfWaitlockRelease**规则指定对[**WdfWaitLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)和[**WdfWaitlockRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)的调用在 KMDF 事件回调函数内按平衡方式使用。 当 KMDF 事件回调函数返回时，驱动程序不应持有通过先前对**WdfWaitLockAcquire**的调用获取的框架旋转锁对象。

**驱动程序模型： KMDF**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>WdfWaitlockRelease</strong>规则。</p>
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

[**WdfWaitLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168) 
[ **WdfWaitLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)
 

 





