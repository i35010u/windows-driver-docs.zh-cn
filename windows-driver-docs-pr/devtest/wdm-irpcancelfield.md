---
title: 'IrpCancelField 规则 (wdm) '
description: IrpCancelField 规则指定该驱动程序在其挂起的 IRP 上设置取消例程时，检查 Irp-Cancel 成员的值。
ms.assetid: e9221436-21ca-47f0-9dc4-e8b1a7a44854
ms.date: 05/21/2018
keywords:
- 'IrpCancelField 规则 (wdm) '
topic_type:
- apiref
api_name:
- IrpCancelField
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9243c87f0ae828e070c2ba4a1c6b8e4d738236c7
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89383189"
---
# <a name="irpcancelfield-rule-wdm"></a>IrpCancelField 规则 (wdm) 


**IrpCancelField**规则指定该驱动程序在其挂起的 Irp 上设置取消例程时，检查**irp- &gt; Cancel**成员的值。

静态驱动程序验证程序将此规则应用到驱动程序的 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio) 例程的末尾，并在驱动程序的调度例程结束时应用。

有关驱动程序应如何处理 IRP 取消的信息，请参阅 [**同步 Irp 取消**](../kernel/synchronizing-irp-cancellation.md)。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IrpCancelField</strong> 规则。</p>
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

[**IoCsqInsertIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp) 
[**IoCsqInsertIrpEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex) 
[**也**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iomarkirppending) 
[**IoSetCancelRoutine**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetcancelroutine)另请参阅
--------

[**同步 IRP 取消**](../kernel/synchronizing-irp-cancellation.md)
 

