---
title: 'IoBuildFsdComplete 规则 (wdm) '
description: IoBuildFsdComplete 规则指定如果 IRP 是使用 IoBuildAsynchronousFsdRequest 创建的，则驱动程序不应调用 IoCompleteRequest。
ms.assetid: 51F3411F-0D59-4341-94C3-8FAF4B98BB3E
ms.date: 05/21/2018
keywords:
- 'IoBuildFsdComplete 规则 (wdm) '
topic_type:
- apiref
api_name:
- IoBuildFsdComplete
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: dbfb4c4c8c628767018b6b3aba421c8ab894aeeb
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89381723"
---
# <a name="iobuildfsdcomplete-rule-wdm"></a>IoBuildFsdComplete 规则 (wdm) 


**IoBuildFsdComplete**规则指定如果 IRP 是使用[**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest)创建的，则驱动程序不应调用[**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。

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
<td align="left"><p>运行 <a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IoBuildFsdComplete</strong> 规则。</p>
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

[**IoBuildAsynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildasynchronousfsdrequest) 
[ **IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest)
 

