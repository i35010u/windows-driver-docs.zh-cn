---
title: ZwRegistryCreate 规则（wdm）
ms.assetid: 7855d9f0-c8f2-42a3-941b-623038c03840
ms.date: 05/21/2018
description: ''
keywords:
- ZwRegistryCreate 规则（wdm）
topic_type:
- apiref
api_name:
- ZwRegistryCreate
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 384ca73e202b068cb7ba05bb8a917908599a2557
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917841"
---
# <a name="zwregistrycreate-rule-wdm"></a>ZwRegistryCreate 规则（wdm）


**ZwRegistryCreate**规则指定在调用[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)之后，驱动程序只能调用以下注册表功能，同时将打开的句柄保存到注册表项（即，在对[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)或[**ZwDeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)的任何调用之前，将句柄关闭或删除到注册表项）：

-   [**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)

-   [**ZwDeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey)

-   [**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey)

-   [**ZwEnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey)

-   [**ZwFlushKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey)

-   [**ZwQueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey)

-   [**ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey)

-   [**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)

此规则还指定，如果驱动程序已经包含一个打开的句柄到该注册表项，则不能调用[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)或[**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey) 。

最后，此规则指定驱动程序在将打开的句柄保存到注册表项时，不能从调度例程或取消例程中返回。

此规则不会验证驱动程序是否已调用[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey)或[**ZwOpenKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenkey)来获取注册表项的句柄，然后再关闭或删除它。

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
<td align="left"><p>运行<a href="https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/static-driver-verifier)">静态驱动程序验证程序</a>并指定<strong>ZwRegistryCreate</strong>规则。</p>
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

[**ZwClose**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose) 
[**ZwCreateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwcreatekey) 
[**ZwDeleteKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwdeletekey) 
[**ZwEnumerateKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratekey) 
[**ZwEnumerateValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwenumeratevaluekey) 
[**ZwFlushKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwflushkey) 
[**ZwQueryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwquerykey) 
[**ZwQueryValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwqueryvaluekey) 
[**ZwSetValueKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-zwsetvaluekey)
 

 





