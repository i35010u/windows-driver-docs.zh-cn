---
title: IoReuseIrp 规则（wdm）
description: IoReuseIrp 规则指定，驱动程序只应在以前使用 IoAllocateIrp 分配的 Irp 上使用 IoReuseIrp。
ms.assetid: E927D12D-03DE-41D7-B130-BA86F0C0CB8A
ms.date: 05/21/2018
keywords:
- IoReuseIrp 规则（wdm）
topic_type:
- apiref
api_name:
- IoReuseIrp
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ff282718fe5d3db049dc3841b80e39e156d26676
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917545"
---
# <a name="ioreuseirp-rule-wdm"></a>IoReuseIrp 规则（wdm）


**IoReuseIrp**规则指定，驱动程序只应在以前使用[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)分配的 irp 上使用[**IoReuseIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp) 。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IoReuseIrp</strong>规则。</p>
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

[**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397) 
[**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402) 
[**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418) 
[**InsertHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist) 
[**IoAllocateIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp) 
[**IoCsqInsertIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirp) 
[**IoCsqInsertIrpEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocsqinsertirpex) 
[**IoInitializeIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeirp) 
[**IoReuseIrp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreuseirp) 
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

 





