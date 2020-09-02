---
title: 'WdfWaitlock 规则 (kmdf) '
description: WdfWaitlock 规则指定对 WdfWaitLockAcquire 的调用用于具有 WdfWaitlockRelease 的 strict 替换项。
ms.assetid: 481c5a21-6c4d-41e3-a54a-3da07d287fda
ms.date: 05/21/2018
keywords:
- 'WdfWaitlock 规则 (kmdf) '
topic_type:
- apiref
api_name:
- WdfWaitlock
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1683b6d9f3e0f1e41e0048e146859532534b2dc2
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381875"
---
# <a name="wdfwaitlock-rule-kmdf"></a>WdfWaitlock 规则 (kmdf) 


**WdfWaitlock**规则指定对[**WdfWaitLockAcquire**](/previous-versions/ff551168(v=vs.85))的调用用于具有[**WdfWaitlockRelease**](kmdf-wdfwaitlockrelease.md)的 strict 替换项。 当 KMDF 事件回调函数返回时，驱动程序不应持有通过先前对 **WdfWaitLockAcquire**的调用获取的框架旋转锁对象。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WdfWaitlock</strong> 规则。</p>
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

[**WdfWaitLockAcquire**](/previous-versions/ff551168(v=vs.85)) 
[ **WdfWaitLockRelease**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)
 

