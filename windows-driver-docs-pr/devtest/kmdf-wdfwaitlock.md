---
title: 'WdfWaitlock 规则 (kmdf) '
description: WdfWaitlock 规则指定对 WdfWaitLockAcquire 的调用用于具有 WdfWaitlockRelease 的 strict 替换项。
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
ms.openlocfilehash: 6dd382bca5e7508ae20b5ca4c77d377a5c8d269c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813249"
---
# <a name="wdfwaitlock-rule-kmdf"></a>WdfWaitlock 规则 (kmdf) 


**WdfWaitlock** 规则指定对 [**WdfWaitLockAcquire**](/previous-versions/ff551168(v=vs.85))的调用用于具有 [**WdfWaitlockRelease**](kmdf-wdfwaitlockrelease.md)的 strict 替换项。 当 KMDF 事件回调函数返回时，驱动程序不应持有先前对 **WdfWaitLockAcquire** 的调用获取的框架等待锁定对象。

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>WdfWaitlock</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**WdfWaitLockAcquire**](/previous-versions/ff551168(v=vs.85)) 
[ **WdfWaitLockRelease**](/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)
