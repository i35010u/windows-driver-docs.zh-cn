---
title: IrpProcessingComplete 规则（wdm）
description: IrpProcessingComplete 规则指定如果派单例程返回状态 \_ SUCCESS，则 IRP 必须已由驱动程序本身或较低级别的驱动程序完成。
ms.assetid: e0dc995e-a5a0-44e3-8cf1-52df8a825598
ms.date: 05/21/2018
keywords:
- IrpProcessingComplete 规则（wdm）
topic_type:
- apiref
api_name:
- IrpProcessingComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4d04c75ffb8ba4c67f292738335a9e8004406e0e
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917611"
---
# <a name="irpprocessingcomplete-rule-wdm"></a>IrpProcessingComplete 规则（wdm）


**IrpProcessingComplete**规则指定如果派单例程返回状态 \_ SUCCESS，则 IRP 必须已由驱动程序本身或较低级别的驱动程序完成。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>IrpProcessingComplete</strong>规则。</p>
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
[**IoCompleteRequest**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 
[**KeWaitForMultipleObjects**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects) 
[**KeWaitForSingleObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject) 
[**PoCallDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-pocalldriver) 
[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)
 

 





