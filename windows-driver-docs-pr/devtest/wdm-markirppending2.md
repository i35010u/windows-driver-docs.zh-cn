---
title: MarkIrpPending2 规则（wdm）
description: MarkIrpPending2 规则指定如果派单例程返回状态 \_ "挂起"，则它已调用也或将 IRP 传递到较低的驱动程序。 有关免费规范，请参阅 MarkIrpPending。
ms.assetid: 91e22348-f5f3-4ba0-b8dd-ec0aa4b1df5e
ms.date: 05/21/2018
keywords:
- MarkIrpPending2 规则（wdm）
topic_type:
- apiref
api_name:
- MarkIrpPending2
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aa541e951ea4fcbd855db82cf53eb9d749ba27d7
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917869"
---
# <a name="markirppending2-rule-wdm"></a>MarkIrpPending2 规则（wdm）


**MarkIrpPending2**规则指定如果派单例程返回状态 \_ "挂起"，则它已调用[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending)或将 IRP 传递到较低的驱动程序。 有关免费规范，请参阅[**MarkIrpPending**](wdm-markirppending.md) 。

**驱动程序模型： WDM**

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>MarkIrpPending2</strong>规则。</p>
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

[**IoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver) 
[**也**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) 
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)另请参阅
--------

[**MarkIrpPending**](wdm-markirppending.md) 
[**正在同步 IRP 取消**](https://docs.microsoft.com/windows-hardware/drivers/kernel/synchronizing-irp-cancellation)
 

 





